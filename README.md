# Rails Sample App on Localhost #
Quickstart rails application for localhost.

## Localhost Considerations ##
These are some special considerations you may need to keep in mind when
running your application on localhost.

### Database ###
Your application is configured to use your Localhost database in
Production mode.

##### Modified Files #####

<table>
  <tr>
    <th>File</th>
    <th>Variable</th>
  </tr>
  <tr>
    <td>config/initializers/secret_token.rb</td> 
    <td>Railsapp::Application.config.secret_token</td>
  </tr>
  <tr>
    <td>config/initializers/session_store.rb</td>
    <td>Railsapp::Application.config.session_store</td>
  </tr>
</table>

## Manual Installation ##

1. Create an account at http://openshift.redhat.com/

1. Create a rails application

    ```
    rhc app create -a railsapp -t ruby-1.9
    ```

   **Note:** To support Ruby 1.8,
   ```
   +++ config/initializers/wrap_parameters.rb
   @@ -5,7 +5,7 @@
    
     # Enable parameter wrapping for JSON. You can disable this by setting :format to an empty array.
      ActiveSupport.on_load(:action_controller) do
      -  wrap_parameters format: [:json]
      +  wrap_parameters ({:format => [:json]})
       end
  ```



1. Add mysql support to your application

    ```
    rhc cartridge add -a railsapp -c mysql-5.1
    ```

1. Add this upstream Rails quickstart repository

    ```
    cd railsapp
    git remote add upstream -m master git://github.com/openshift/rails-example.git
    git pull -s recursive -X theirs upstream master
    ```

1. Push your new code

    ```
    git push
    ```

1. That's it! Enjoy your new Rails application!


[template]: https://openshift.redhat.com/app/console/application_types/rails

License
-------

This code is dedicated to the public domain to the maximum extent permitted by applicable law, pursuant to CC0 (http://creativecommons.org/publicdomain/zero/1.0/)
