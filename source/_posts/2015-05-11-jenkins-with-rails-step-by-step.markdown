---
layout: post
title: "Jenkins with Rails step-by-step"
date: 2015-05-11 13:38:52 +0300
comments: true
categories: ci
---

In [my previous post](http://goodniceweb.me/05-04-2015/jenkins-rails-docker-container.html)
you can find manual of jenkins-rails container usage. Here I want to extend it,
add some screenshots and so on.

At first, let's create new rails app.

<!-- more -->

```bash
$ rails --version
Rails 4.2.0.rc2
$ rails new candy --skip-test-unit && cd candy
$ git init && git add . && git ci -m "Initial commit"
```

Now I'll install `rspec` and make get some dead simple tests from scaffold.

[Gemfile](http://pastie.org/private/nuhg3wvcphhc0euzkd4tw)

```bash
$ rails g rspec:install
$ rails g scaffold article title content:text
$ rake db:migrate
$ echo '-f documentation' >> .rspec
$ rspec spec
```

Last will must return smth. like this

```bash
Finished in 0.2916 seconds
30 examples, 0 failures, 2 pending
```

Than let's execute line from previous post.

```bash
$ docker run -d \
    -p 8080:8080 \
    -v ~/your/folder:/home/jenkins_home \
    --name jenkins \
    goodniceweb/jenkins-rails:latest
```

Now on visiting [http://localhost:8080/](http://localhost:8080/) you'll see Jenkins dashboard screen.
#screenshot

At first here I propose to make Jenkins more secure. Click to "Manage Jenkins" link
and than to "Setup Security" button. On opened page check "Enable security" box.

#screenshot

In "Access Control" section "Security Realm" sub-section choose "Jenkins’ own user database" radiobutton.
Below, in "Authorization" sub-section choose "Project-based Matrix Authorization Strategy" option. 

#screenshot

You'll able to see created table with only 'Anonymous' user for now. We will fix it later.
At first let's add 'Read' permission to Anonymous user. Just tick according checkbox.

#screenshot

Ok, now the time for creating admin user. Focus this input...

#screenshot

... write 'admin' and press "Add" button. Then scroll horisontally, if its need, 
and press on this little icon. All checkboxes should be chosen for admin, right?

Perfect. Now I propose to save your changes. Press "Save" button underneath. 
You should be redirected to login page after this because now you are Anonymous user.
Don't worry, directly after registration you'll able to continue configuring Jenkins.

# screenshot

Super awesome. Now time to initialize our project. Press "create new jobs" on main page 
or "New Item" link. Than choose a name and select "Freestyle project" option. Press "OK".

#screenshot

Then you'll see Job Settings page. Few things here need to be configured:

1. Security settings. Add your 'admin' user with all permissions.
2. Choose "Git" from "Source Code Management" section. Install your credentials.
   I prefer to use https with login/password for this test.
3. Install push hooks and rvm settings.
4. Insert build script for testing project

   I prefer to use smth. like this:

   ```bash
   bundle install --without production --deployment
   cp -f config/database.yml.example config/database.yml
   cp -f config/secrets.yml.example config/secrets.yml
   bundle exec rake db:migrate RAILS_ENV=test 
   bundle exec rspec spec 
   ```

   Here we make sure that we had latest gem and database settings.
   Also we place secrets.yml file, update db state and run the tests.

5. Let's create email notification for failing cases.

That's it. Pressing "Save" button will redirect us to main Job page.




