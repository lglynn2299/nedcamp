# nedcamp

This is the README for the New England Drupal Camp website.

### Server and workflow 

The site is hosted on Pantheon. You must have a Pantheon account and have that account added to this site to access the dashboard. 

Repo: git@github.com:NEDCamp/nedcamp.git

On Pantheon sites, the master branch is used on the dev, test and live environments.

Dev:  http://dev-nedcamp.pantheonsite.io/  
user/pass to unlock is (ask). 

Normally there will also be a staging branch and environment, but at this time that are not setup yet.

Once everything is setup, normal workflow is shown below. See this Pantheon doc for more:  https://pantheon.io/docs/guides/build-tools/new-pr/ 

- Create a feature branch off of master branch. You may want to give that branch your name.
- Do work in that features branch.
- When you like the work on local, push that branch `git push origin name` where `name` is the name of your branch.
- Note this will automatically create an environment on Pantheon:  http://id-nedcamp.pantheonsite.io  ...so you can check it out there also. 
- On Github, do a pull request to pull your branch `name` into `master`. 
- When the pull request is approved and merged it will deploy to the dev site:  http://dev-nedcamp.pantheonsite.io/

From Pantheon:
"Once your tests have passed, and there is nothing else that you wish to add to this particular feature, click on the Merge Pull Request.
When your Pull Request is merged, one more test run will be started to test the result of combining the code and configuration from your Pull Request with the master branch. Once this test passes, the configuration for your site will be applied to the Dev environment, and the corresponding Multidev environment will be deleted. Note that database content is not merged; make sure that you have exported your configuration before merging your Pull Request to ensure that configuration changes are not lost.
You may now use the Pantheon dev / test / live workflow to deploy your site as usual. Continue reading this guide to learn how to manage core updates and create a custom theme."
See: https://pantheon.io/docs/guides/build-tools/merge/

At this point, there is no test and live, we will be working just with dev, and with staging once that is setup. 

The workflow uses CircleCI, so pushing to Github triggers a push to CircleCI then to Pantheon. 


### Set up your local (with MAMP or whatever) 

1. Clone the repo.
2. cd into the folder you cloned into, and run `composer install`
3. Create a local database and import a dump from Pantheon dev into it (get that from the Dashboard).
4. Copy the `_docs/settings.local.php` to `/web/sites/default/settings.local.php` and adjust database name, user and password. 
5. The repo does not come with an .htaccess file becuase Pantheon uses NGINX so copy `_docs/.htaccess` to `/web/.htacess` if you run Apache locally.
6. The user/1 user/pass is in LastPass.

### Set up you local with Lando

- Clone the repo.
- cd into the folder you cloned into, and run `composer install`
- Install Lando if you do not alreayd have it: https://docs.devwithlando.io/installation/installing.html
- from within the folder that you cloned the repo into, run `lando start`

- after it starts, run `lando info`

- to get info about where the database is, which will look like this:

```
"database": {
    "type": "mariadb",
    "version": "10.0",
    "creds": {
      "user": "pantheon",
      "password": "pantheon",
      "database": "pantheon"
    },
    "internal_connection": {
      "host": "database",
      "port": 3306
    },
    "external_connection": {
      "host": "localhost",
      "port": "32770"
    },
    "config": {
      "confd": "/Users/rick/.lando/services/config/pantheon/mysql"
    }
  },  
```
- To connect to the database with Sequel Pro (or similar use localhost, the creds as shown, and port 32770 (note yours may be different). 

- If you have been given access to the Pantheon dashoard, you should be able to run the command `lando pull`  It will ask you what site to pull from (probably will just list nedcamp) and whether you want to pull code (say no, you already have it) or database (say yes) or files (optional). 

### Set up you local with Docksal

Mike added files to use Docksal on local.

Run `fin init` in the site root. 





