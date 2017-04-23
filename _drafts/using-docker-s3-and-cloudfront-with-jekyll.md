---
layout: post
title: Using Docker, S3, and Jekyll To Run Your Blog
# target: Docker, S3 and Jekyll
---


[Docker](https://www.docker.com) is an absolutely amazing paradigm when it comes to compartmentalizing an application. This makes Docker particularly impressive when it comes to deploying an application but since its a completely self contained environment, I'm a big fan of using Docker for development as well.

My obsession with compatmentilization was driven into me when I was taking CS classes in college. Professors would say "you never want to polute the global namespace". Yet much of the time when I sat down to start work on application I would install all of the dependencies required for development directly into my os.

Although I've never run into a specific problem with doing things this way it always felt a bit "dirty" to me since managing different versions of ruby/python/node/etc always seemed like a bit of a pain.

For the longest time I really had no choice but fortunately these days our machines are powerful and have lots of memory so we can start to think about encapsulating all of our dependencies within the application.

Thanks to [Docker](https://www.docker.com) I've been able to clean up my OS instal and effortlessly develop without needing to run "ruby -v" or anthing similar.

### Why use Docker for Jekyll? Isn't that overkill?

I guess you could consider it a bit overkill to roll a [Docker](https://www.docker.com) container for something as simple as Jekyll but I think the better question to ask is "why not".

Arguments against running Jekyll in [Docker](https://www.docker.com):

- It's easy to install RVM and get nearly any version of Ruby setup
- Jekyll is less of an application and more of a script that compiles a webpage
- Docker images can sometimes take up a lot of space
- Docker has a learning curve

Yes it may be easy to setup RVM and Ruby, but it's even easier to setup Ruby inside of Docker. Plus once you get a Dockerfile built you can just copy and paste for all future Ruby projects. Using something like "docker-compose" can greatly ease the implimentation and learning curve of Docker since you wont need to do manual linking of containers, networks, etc.

Here are a few things you gain from rolling your own Docker container:

- The dependencies go along with your app (Jekyll in this case) so as long as you have Docker installed building/editing a site is very simple
- When you decide to build the app, it will build exactly like it did on your machine. This comes in handy if you want to deploy to S3 automatically.
- Once you get Docker installed, it's trivial to get the version of Ruby you need installed
- TODO: Some other option

This guide will show you how to setup a Jekyll within docker image so that you can easily manage your blog site without needing to download and install dependencies.

### Setting Up Key Tools

#### Docker and docker-compose
Getting Docker setup in the first place is super simple if you are on macOS. All you need to do is head over to the [Docker engine install page](https://docs.docker.com/docker-for-mac/) to download an app and install it. One thing to note when you are doing a macOS install Docker is running inside of a VM and you can easily tweak the memory allocation and number of cores.

TODO: Include image of the config panel

If you are doing a [Linux Docker install](https://docs.docker.com/engine/installation/) things can be slightly more complex depending on your distribution.

```
docker-jekyll/
├── Dockerfile
├── docker-compose.yml
├── Gemfile
```

Once you have Docker installed, the first step is to get your [Dockerfile](https://docs.docker.com/engine/reference/builder/) setup. Essentially the Dockerfile is a configuration script that is used to build your image. This allows you to do things like set the distribution of Linux you want to use, download a specific version of Ruby, etc. The Dockerfile should be places in the root of your directory.

The "docker-compose.yml" file is a configuration file that is used by docker-compose which allows you to build very sophisiticated docker arcitectures and with a very simple interface. Fortunately the docs on [docker-compose](https://docs.docker.com/compose/compose-file/) and the [Dockerfile](https://docs.docker.com/engine/reference/builder/) are very good and I would recommend that you scan through them.

Within the "Gemfile" all we need is "gem jekyll" since it will be used to bootstrap the entire project. This Gemfile will be overwritten by the jekyll install script.

TODO: Put Dockerfile example here https://github.com/jsmootiv/docker-jekyll/blob/master/Dockerfile
TODO: Put walkthrough of the file here also

Once you have everything downloaded and installed just run the Jekyll init script through docker-compose run and Docker will go off and pull down all of the requirements to get you started.

	```
	docker-compose run serve bundle exec jekyll new .
	```

#### Optional SEO Tweaks

There is a lot of debate in SEO circles with reguard to the importance of setting your blog up as a subdomain eg "blog.octaviuslabs.com" vs a directory off of your main site eg "www.octviuslabs.com/blog".

I generally beleive that its best practice to setup the blog as a subdirectory since it looks a bit cleaner in the URL. For the purposes of the rest of this post I will assume that your goal is to setup jekyll under the /blog subdirectory of your main marketing site.

As such, you will need to make the below change to your "_config.yml" file.

```
baseurl: "/blog" # make sure that this is set to /blog
url: "https://www.octaviuslabs.com"
```

In addition to the directory trick, its usually a best practice to simplify the permalink structure. I choose to

```
permalink: /:title/ # Be sure to include the trailing slash,
						# this makes it so Jekyll creates the file
						# for the post under /{post tile/index.html
						# which comes in handy on deployment
```

#### Working with Jekyll

Now that we have Jekyll setup this next step it's time to start working on some content. Thakfully I've setup the docker-compose file

Remember however that if you ever need to run something on docker.

- if you update the gemfile do a rebuild of the image

TODO: Include readme from github here

TODO: explain why to exclude the below files
```
exclude:
  - Gemfile*
  - Dockerfile
  - docker-compose*
  - .git*
  - Readme*
  - vendor/
  - circle
```

TODO: Add seo gems and such


- S3
  - Setting up a bucket
  - Setting up a ci user w/ right permissions
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:ListAllMyBuckets"
            ],
            "Resource": [
                "arn:aws:s3:::*"
            ]
        }
    ]
}
```


```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": [
                "arn:aws:s3:::octavius-blog",
                "arn:aws:s3:::octavius-blog/*"
            ]
        }
    ]
}
```


  - Giving users persmissions
- CircleCI

There are a lot of people who do their "jekyll build" step locally and then deploy the contents of .site into s3 as perscribed by the Jekyll docs. There is nothing wrong with doing this way and in fact early on its usefull to do just to get a feel for how the application works.

One of my favorie enginnering professors in college once said "the best engineers are lazy" and I whole hartedly agree. If you are doing a build as well as saving the source to GitHub that means you are writing 4 commands for every build.

1. docker-compose run build
2. take contents of .site and put them on s3
3. git add new-post.md
4. git commit -m "added post on foo"
5. git push origin master

If you are like me you probably think that the first 2 steps are a bit of a hastle. Why not just have co do them for you.

Thats where [CircleCI](https://circleci.com) becomes useful. By pointing CircleCI at your github repo and writing a custom circle.yml file you only need to write the build step onece then every time you push your code upto github CircleCI will pull down your code, do the build and push the resulting site up to s3 for you. This entirely eliminates step 1 and 2 above.

So what does a cirlce.yml look like? Let me show you.
  - https://github.com/jsmootiv/docker-jekyll/blob/master/circle.yml

The yml file is broken up into a few differnt stages.
```
machine:
  ruby:
    version: 2.3.0

dependencies:
  override:
    - bundle install
    - bundle exec jekyll build

test:
  override:
    - echo "This is the only test and it does nothing"

deployment:
  prod:
    branch: master
    commands:
      - aws s3 sync ./_site s3://{{REPLACE WITH BUCKET}}/blog --delete

```

Is a bit obvious it just bulds a machine with ruby version 2.3.0. The next block

  - circle.yml walkthrough


- Cloudfront

At this point you tecnically could serve your website directly from S3.

  - Direct the domain to the blog url (be sure to setup a custom record, not an s3 record)
  - Setup a redirect bucket in s3

- Route53 Configuration
  - Wait for cloudfront to be ready
  - Connect the sites


- Git/Github (alternative setup)
  - Host the source of the document
  - Delete the circle.yml (you dont need it)
