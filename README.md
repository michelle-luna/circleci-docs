# CircleCI Documentation [![CircleCI Build Status](https://circleci.com/gh/circleci/circleci-docs.svg?style=shield)](https://circleci.com/gh/circleci/circleci-docs) [![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/circleci/circleci-docs/master/LICENSE) [![CircleCi Community](https://img.shields.io/badge/community-CircleCI%20Discuss-343434.svg)](https://discuss.circleci.com)

This is the public repository for <https://circleci.com/docs/>, a static website generated by [Jekyll](https://jekyllrb.com/). If you find any errors or have requests, you can contribute by:

1. reading our [Contributing Guide](CONTRIBUTING.md)
1. setting up a local environment using the instructions below

If you can't contribute but still want to report a problem, open an [Issue](https://github.com/circleci/circleci-docs/issues) on this project. If you have a question or need help debugging a problem, **do not submit an issue**. Instead, please head to [CircleCI Discuss](https://discuss.circleci.com/), and our support team will help you out.

## Local Development
There are two ways to run a local development server: [with Vagrant](#with-vagrant) or [without Vagrant](#without-vagrant).

### Without Vagrant
If you already have a stable Ruby environment and feel comfortable installing dependencies, you can run the server directly on your machine.

#### Prerequisites
- Ruby: see this project's Gemfile for the version of Ruby currently being used with this project. We recommend RVM for managing multiple Ruby versions, but there are other options available
- [Jekyll](https://jekyllrb.com/): Jekyll 3
- [HTMLProofer](https://github.com/gjtorikian/html-proofer): used for testing links, images, and HTML. The docs site will need a passing build to be deployed, so use HTMLProofer to test everything before you push changes to GitHub.

You're also welcome to use Bundler to install required gems. If you are using RVM (or similar), make sure they all play nicely together.

#### First Run
To get a local copy of <https://circleci.com/docs/>, run the following commands:

```bash
git clone https://github.com/circleci/circleci-docs.git
cd circleci-docs/jekyll
jekyll serve
```

Jekyll will build the site and start a web server, which can be viewed in your browser at <http://localhost:4000/docs/>.

####  Editing Docs
Please see the `CONTRIBUTING.md` file in this repository for information on working on the documentation.

## Jekyll Commands
`jekyll build`: generates static files for the site in the `jekyll/_site` directory

`jekyll serve`: runs `jekyll build`, then starts an included mini webserver to serve files from `'jekyll/_site`; listens to
localhost:4000 by default

`jekyll serve --detach`: this serves the site as before, but runs in the background so you can use the same terminal window. Jekyll will display its process ID, so you can use that to kill the process when you want to stop Jekyll. If you lose the PID, you can run `pkill -f jekyll` to kill all Jekyll instances.

### With Vagrant
The easiest way to get started is by using Vagrant, which gives you a clean environment with all necessary dependencies.

#### Prerequisites
- Vagrant: [download directly](https://www.vagrantup.com/downloads.html), `brew cask install vagrant`, or `sudo apt-get install vagrant`
- VirtualBox: [download directly](https://www.virtualbox.org/wiki/Downloads), `brew cask install virtualbox`, or `sudo apt-get install virtualbox`

#### First Run
To get a local copy of <https://circleci.com/docs/>, run the following commands:

```bash
git clone https://github.com/circleci/circleci-docs.git
cd circleci-docs
./jctl start
```

The first time you run `./jctl start`, Vagrant will provision the entire VM based on the contents of `boostrap.sh`. This process can take a few minutes, but it's a one-time deal.

Once this is complete, Jekyll will automatically start in the VM. Vagrant will then begin forwarding port 4040, and you'll be able to view the docs at <http://localhost:4040/docs/>.

####  Editing Docs
Please see the `CONTRIBUTING.md` file in this repository for information on working on the documentation. When running in vagrant, if you make changes, run `./jctl rebuild` to have Jekyll rebuild the site. For more detailed instructions on using `jctl`, see [below](#jekyll-controller-jctl).

As an alternative to `jctl`, you can log into the VM directly to interact with Jekyll. Run `vagrant ssh` to enter the VM, then `cd /vagrant/jekyll` to access the repository's files. From there, you can run standard Jekyll commands with any preferred options.

## Jekyll Controller (`jctl`)
This is a Bash wrapper script to talk to Jekyll & Vagrant.

- `start`: starts Jekyll; will also start Vagrant, if not already running
- `rebuild`: rebuilds the site
- `stop`: shuts down entire VM (including Jekyll)
- `restart`: `./jctl stop && ./jctl start`

## License Information
Documentation (guides, references, and associated images) is licensed as Creative Commons Attribution-NonCommercial-ShareAlike CC BY-NC-SA. The full license can be found [here](http://creativecommons.org/licenses/by-nc-sa/4.0/legalcode), and the
human-readable summary [here](http://creativecommons.org/licenses/by-nc-sa/4.0/).

Everything in this repository not covered above is licensed under the [included MIT license](LICENSE).
