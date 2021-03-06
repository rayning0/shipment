# Shipment

Easy deployment using Docker

## Installation

    $ gem install shipment-deploy

## Usage

    $ ship lash # Setup credentials

    $ ship this # Prepare application for deployment

    $ ship out  # Deploy application

    $ ship logs # View logs

## What It Does

1. Sets up a droplet on DigitalOcean with the proper SSH key
2. Creates two Docker containers on the droplet: one for your
   application, and one for a Postgres database
3. Sets up a deploy key for your application's repo on GitHub
4. Adds a `.shipment` file to your project containing
   application-specific information
5. Adds an entry to a global `.shipment` file in your home directory to
   keep track of all deployments

## Notes

1. Setup takes between 5 and 10 minutes, depending upon the speed of
   DigitalOcean
2. During setup, green arrows indicate local ouptut, blue arrows
   indicate commands run on the server, red arrows indicate failed
commands and/or connection timeouts, and unmarked output represents
stdout on the server.
3. Some output is printed in red, even though there is no error. Some
   server output is being improperly redirected to stderr.
4. Currently, the only option is to set up a 2gb droplet in the NYC2
   region.
5. Currently, the server runs on port 3000.

## Todo

1. Only add `.shipmet` to `.gitignore` once, duh!
2. Handle SSH authorization issues when re-setting up. DigitalOcean
   allows adding multiple keys with the same name. Need to delete
existing key locally and remotely when running setup again. (Probably
should either remove `ship setup` command or do some checking when that
command is run.)
3. Need to deal with commit limit. Containers need to be exported every
   once in a while to clean up Aufs layers.
4. Save and push application-specific docker images to user's docker
   account.
5. Allow deploying from branches other than master.
6. Error handle *way* better. Need to be able to handle partial
   setups/deploys.
7. Look into creating a base image that already includes ruby and
   postgres containers. (Requires support from DigitalOcean.)
8. Better deal with committing and pushing on `ship this`. Right now,
   rejected pushes would break everything.
9. Create simple way to symlink credentials from an `application.yml` or
   `.env` file.
10. Fix messy output during setup and deploy. Also, deal with duplicate
   'Done.'s when a command is re-run.
11. Speed everything up.
12. Clean up the classes. Most things are doing *way* too much.
13. Write specs!
14. Add cleanup option to remove all system config.

## Contributing

1. Fork it ( https://github.com/loganhasson/shipment/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request

# Author

[@loganhasson](http://twitter.com/loganhasson)

