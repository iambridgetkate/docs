+++
title="An App's Brief Journey from Source to Image"
weight=2
creatordisplayname = "Andrew Meyer"
creatoremail = "ameyer@pivotal.io"
lastmodifierdisplayname = "Andrew Meyer"
lastmodifieremail = "ameyer@pivotal.io"
+++

## `pack` for the journey

In this tutorial, we'll explain how to use `pack` and **buildpacks** to create a runnable app image from source code.

That means you'll need to make sure you have `pack` installed:
<br/><br/>
<a href="/docs/install-pack" class="download-button button icon-button bg-pink">Install pack</a><br/>

> **NOTE:** `pack` is only one implementation of the [Cloud Native Builpacks Platform Specification][cnb-platform-spec].

[cnb-platform-spec]: https://github.com/buildpack/spec/blob/master/platform.md

## Buildpack base camp

Before we set out, you'll need to know the basics of **buildpacks** and how they work.

### What is a buildpack?

A buildpack is something you've probably leveraged without knowing, as they're currently
being used in many cloud platforms. A buildpack's job is to gather everything your app needs to build and run,
and it often does this job quickly and quietly.

That said, while buildpacks are often a behind-the-scenes detail, they are at the heart of transforming your source
code into a runnable app image.

### Auto-detection

What enables buildpacks to go unnoticed is auto-detection. This happens when a platform sequentially
tests groups of buildpacks against your app's source code. The first group that deems itself fit for your source code
will become the selected set of buildpacks for your app. Detection criteria is specific to each buildpack -- for
instance, an **NPM buildpack** might look for a `package.json`, and a **Go buildpack** might look for Go source files.

Let's see auto-detection in action by running `pack build` against a simple Java app.

## Next stop, the end

Run the following commands in a shell to clone and build this [simple Java app](https://github.com/buildpack/sample-java-app).

```bash
git clone https://github.com/buildpack/sample-java-app.git
cd sample-java-app
pack build myapp
```

> **NOTE:** This is your first time running `pack build` for `myapp`, so you'll notice a couple of things:
> <br/><br/>
> **A message about selecting a default
> [builder](/docs/using-pack/working-with-builders).** A builder is essentially an image containing buildpacks. Follow
> the provided instructions to select one, then run `pack build myapp` again.
> <br/><br/>
> **The build might take longer than usual.** Subsequent builds will take advantage of various forms of caching.
> If you're curious, try running `pack build myapp` a second time to see the difference in build time.

**That's it!** You've now got a runnable app image called `myapp` available on your local Docker daemon.
We did say this was a *brief* journey after all. Take note that your app was built without needing to install
a JDK, run Maven, or otherwise configure a build environment. `pack` and **buildpacks** took care of that for you.


## Beyond the journey

To test out your new app image locally, you can run it with Docker:

```bash
docker run --rm -p 8080:8080 myapp
```

Now hit `localhost:8080` in your favorite browser and take a minute to enjoy the view.

### Take your image to the skies

`pack` uses **buildpacks** to help you easily create OCI images that you can run just about anywhere. Try
deploying your new image to your favorite cloud!

> In case you need it, `pack build` has a handy flag called `--publish` that will publish your app image to a Docker
> registry after building it.
