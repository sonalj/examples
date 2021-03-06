DataNucleus Example Application
===============================

This example builds a simple application based on DataNucleus using the JDO API.

BUILD INSTRUCTIONS
------------------

Run the build by invoking `ant -f build/build.xml`. Artifacts will be
generated, along with a Nimble index file, in the `cnf/releaserepo` directory.

DEPLOY/RUN
----------

Run the supplied automation script as follows: `posh -k cnf/load-system.osh`. This will start a fibre, load repositories, import and deploy the system.

SHELL INTERACTION
-----------------

The example includes simple shell commands to interact with the database via DataNucleus:

* `blog:list` lists all the comments entered on a hypothetical blog site.
* `blog:create <comment>` enters a new comment.

For example:

    % blog:create "Hello world"
    % blog:list
    Listing 1 comments:
    Sep 21 20:44:22 BST 2012 :: Hello world
    END

REST INTEGRATION
----------------

Comment listing and posting operations are available via a RESTful service at URL
`http://hostname:9000/blog/comments.

* `GET /blog/comments` returns a list of all available comments
* `GET /blog/comments/<id>` returns details of the comment with the specified ID.
* `PUT /blog/comments/<id>` updates the comment with the specified ID, or creates
  new comment with that ID if none existed.
* `POST /blog/comments` creates a new comment with a generated ID.


CAMEL INTEGRATION
-----------------

The example includes an Apache Camel component that allows blog comments to be created by
posting files in a directory.

A directory named `INBOX` will have been created underneath the current running directory.
Create a file with any name in that directory, with the following content:

    {"id":"1234", "text":"Nice blog!"}

The fill will be processed by Camel and immediately moved into the `.done` subdirectory.
You can then view the new comment via the shell or REST interface.

PLAY APPLICATION
----------------

The example includes a front-end application, built with the Play Framework and packaged
with the Paremus Packager. It can be accessed by opening the URL:

  http://localhost:9999/


