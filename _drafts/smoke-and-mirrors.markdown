---
layout: post
title: "Smoke and Mirrors"
date: 2015-08-28T17:44:29+02:00
---

At [Savedo](https://www.savedo.de), one of my tasks included to create a smoke test suite. Being familiar with [Capybara](https://github.com/jnicklas/capybara) and [RSpec](http://rspec.info/), I used these tools for that tasks. Here's how.

## Smoke tests?

You have lots of unit tests and a reasonable amount of feature tests. Why should you care to have another test suite?

Well, for one, your CI server runs your doesn't run your production website. Having the tests pass on CI thus doesn't necessary mean that the site is up and running after the deploy. Many developers manually check the basic functionality of a website after they deployed. Smoke test verify the deploy in an automated way.

If you follow a [Blue Green Deployment](http://martinfowler.com/bliki/BlueGreenDeployment.html) strategy or bring up new virtual servers for each deploy (see [Immutable Infrastructure](http://chadfowler.com/blog/2013/06/23/immutable-deployments/)), you could even run the tests before the new servers are enabled in the load balancer.

And if your application consists of multiple services, your tests probably stub the service boundaries, possibly with some contract testing. Smoke tests ignore the service boundaries, thus integration testing the entire site.

However, as smoke tests are pretty high level, I believe that they should test just the core functionality of your application. Is it a shop? Let them buy some 2 $ item (You can cancel the order in a later step). Is it required to sign in? Let the tests make sure, registration and login still work. In Savedo's case, they for now sign up for a fixed deposit account and check the generated PDF.

## Let's get started!

In my previous job, we used [Watir](http://watir.com/) for smoke testing. However, as a developer I write tests with RSpec and Capybara all day, why should learn new tools to do almost the same thing? Using [Selenium](http://www.seleniumhq.org/) however makes sense to me, as it allows me to use all major browsers and I can follow along the test run when I run it in non-headless mode.

Ok, lets create a `Gemfile`:

{% highlight ruby %}
source "https://rubygems.org"

gem "capybara"
gem "selenium-webdriver"
gem "rspec"
{% endhighlight %}

Next, we need to configure the Capybara to not start a webserver for us. After running `rspec --init`, drop this in your `spec/spec_helper`:

{% highlight ruby %}
require 'capybara/rspec'
require 'selenium-webdriver'

Capybara.default_driver = :selenium
Capybara.run_server = false
Capybara.app_host = "https://google.com" # Adjust this
Capybara.default_max_wait_time = 15

RSpec.configure do |config|
  config.include Capybara::DSL
end
{% endhighlight %}

And off you go to write specs:

{% highlight ruby %}
require 'spec_helper'

RSpec.describe "Google" do
  it "Searches for Ruby and sees the right page" do
    visit '/'

    fill_in "q", with: "Ruby programming language"

    expect(page).to have_content("https://www.ruby-lang.org")
  end
end
{% endhighlight %}

Now dare to run it:

~~~
$ rspec spec/google_spec.rb
.

Finished in 5.64 seconds (files took 0.29854 seconds to load)
1 example, 0 failures
~~~

You should have seen a Firefox window opening, going to google.com and entering "Ruby programming language" into the search field. The result is a green dot. Success!

![](/img/smoke_yay.gif)

## Analyze failures

First a small but useful trick: Let RSpec take a screenshot of the browser when a spec fails! It's easy to do and usually it also gives you a pretty good idea what went wrong. Again, open the `spec/spec_helper.rb` and add this:

{% highlight ruby %}
RSpec.configure do |config|
  config.after do |example|
    take_screenshot_on_failure(example)
  end
end

# Will store a screenshot and the page HTML in artifacts when a feature spec
# failes. The name of these files is generated from the spec path and line
# number. E.g. a failure in:
#   spec/login_spec.rb:14
# will generate:
#   artifacts/login_spec.rb_14.html
#   artifacts/login_spec.rb_14.png
def take_screenshot_on_failure(example)
  if example.exception
    file_base = "#{example.metadata[:file_path][7..-1].gsub('/', '_')}_#{example.metadata[:line_number]}"

    File.write("artifacts/#{file_base}.html", page.html)
    page.save_screenshot("artifacts/#{file_base}.png", full: true)
  end
rescue
  warn 'Screenshot taking failed...'
end
{% endhighlight %}

Lets look at a few typical failure sources. Having JavaScript or CSS transisions involved is a big one, but I fear we're not going rid of these just to make our tests more stable.

Sometimes you need to wait with an action for something else. Many resort to introduce `sleep`s in their tests. I try to avoid them as long as possible. The time to sleep is usually choosen by a gut feeling. 

## Cleaning up


