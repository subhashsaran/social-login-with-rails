# Devise + Facebook Login + Google Login + Twitter Login + Linkedin Login + Github Login
Basic application with all the popular Social login System.

## Demo

[Live Demo for rails 3.2.15 and Foundation Framework](http://social-login-in-rails.herokuapp.com/) (Code lies on tag rails-3.2.15-foundation)

For rails 4.2.3 and Twitter bootstrap - Pull the code from master branch

## Gems Used

* devise
* zurb-foundation (For Rails 3.2.15 version)
* Twitter Bootstrap (For Rails 4.0.2 version)
* carrierwave
* twitter
* jquery-rails
* json
* koala
* linkedin
* omniauth
* omniauth-facebook
* omniauth-github
* omniauth-google-oauth2
* omniauth-linkedin
* omniauth-twitter
* rmagick

Add following line to your devise.rb File

app/config/initializers/devise.rb

Devise.setup do |config|
...
  config.omniauth :facebook, "KEY", "SECRET"
  config.omniauth :twitter, "KEY", "SECRET"
  config.omniauth :linked_in, "KEY", "SECRET"
...
end

Paste this line in your routes.rb file

config/routes.rb

 devise_for :users, :controllers => { omniauth_callbacks: 'omniauth_callbacks' }

Now Create a controller to handle the callback from social websites

Create app/controllers/omniauth_callbacks_controller.rb

It’s worth mentioning that the only safe criteria for matching user entities with OAuth providers is a verified email address, but this will lead to the creation of multiple accounts if the user has different email addresses associated with different OAuth providers. Let’s say, for example, the user registers with Facebook, and then later tries to signin with a LinkedIn account that has a different email address associated, the system can only create a new account because there’s no way to match the existing user entity with the LinkedIn account.

Therefore, to link accounts with multiple providers the current_user session must be already set when the OAuth callback returns, and passed to User.find_for_oauth. This might sound complicated, but all thats required to link a different provider, Facebook for example, is to redirect_to user_omniauth_authorize_path(:facebook) while the user is already logged in.



Completing the Signup Process

Most OAuth providers give us all the information we need, but if the user signed up with Twitter, or perhaps for some reason the OAuth provider didn’t provide a verified email address, or maybe you just want to get some extra information from the user, then we need to implement an extra step for this
