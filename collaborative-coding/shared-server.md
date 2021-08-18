# Using a Shared server

## Create a remote server
TODO: how to create a suitable remote server on AWS, Google, etc.

> Dont forget to switch the server off when not using it, so it doesnt cost you extra credits.


## Install Clojure
Use the Clojure.org Getting Started instructions to download Clojure for Linux and run the install script.  This installs `clojure` command system wide (`/usr/local/bin/`) along with the `clj` wapper that runs a terminal REPL using `rlwrap` (TODO: check rlwrap is installed).

Use a range of community tools by installing the practicalli/clojure-deps-edn configuration (first deleting the `~/.clojure` directory if it exists - create if you run `clojure` or `clj` for the first time)

```
git clone https://github.com/practicalli/clojure-deps-edn.git ~/.clojure/
```

New projects can be created on the remote server, using one of the numerous [project templates for Clojure projects](https://practicalli.github.io/clojure/clojure-tools/projects/create.html).  For example a simple command line application

```
clojure -X:project/new :template app :name scicloj/my-app
```

Run a feature rich terminal REPL using rebel readline

```
clojure -M:repl/rebel
```


## Configure the SSH connection
Generate a permissions file, `.pem` from the server (TODO: how to generate .pem files) and save it to `~/.ssh/` directory (or your preferred location).

Edit the `~/.ssh/config` file (create the file if needed) and add a host configuration for the remote server.

Add the IP address of the remote server to `HostName`.

Use the `LocalForward` for the port used by the nREPL server.

```
Host remote-clojure-server
  HostName 99.99.99.99
  IdentityFile ~/.ssh/remote-server.pem
  User ubuntu
  PasswordAuthentication yes
  LocalForward 1234 localhost:1234
  Port 22
```

## Starting a REPL with Editor support
The majority of [Clojure aware editors](https://practicalli.github.io/clojure/clojure-editors/) can connect to an external REPL using the nREPL protocol.  Emacs CIDER, VSCode Calva and NeoVim Conjure all use nREPL and the Cider middleware.

The `:middleware/cider-clj` will inject the nREPL and Cider middleware libraries.

SSH into the remote server.

Change to a Clojure project

Start the REPL using the cider middleware on the same port as defined in `LocalForward` in the SSH configuration, using the `-p` to set the port number.

```shell
clojure -M:middleware/cider-clj -p 1234
```


## Configure Emacs to listen to nREPL port
Emacs can be used to connect to a running Clojure project that has been run with the nREPL and Cider middleware, e.g. `:middleware/cider-clj` from [`practicalli/clojure-deps-edn`](http://practicalli.github.io/clojure/clojure-tools/install/community-tools.html)

Edit your Emacs `~/.emacs.d/init.el` file and add the following configuration.

For Spacemacs, edit `~/.spacemacs` and add the following code to `dotspacemacs/user-config`

```elisp
  (setq nrepl-use-ssh-fallback-for-remote-hosts t)
```


## Using NeoVim and Conjure on remote server
NeoVim and Conjure are installed on the remote server using the [Practicalli install guide](https://practicalli.github.io/clojure/clojure-editors/editor-install-guides/neovim-conjure.html).

Conjure will automatically connect to a running REPL

> #### Hint::Conjure uses .nrepl-port
> Conjure looks for the `.nrepl-port` in the root of the project.  If this file is not created when running the REPL, create the file and use the same value as `LocalForward` from the SSH configuration.


## Apache HTTPd server as a reverse proxy
Use a reverse proxy if you wish to expose visualizations via a browser, such as Oz or notespace.

ssh into the remote server with an account that has sudo privileges

Enable the reverse proxy module `mod_proxy_http` which has a dependency on `mod_proxy` and is also enabled automatically.

```shell
sudo a2enmod proxy_http
```

> #### Hint::Modules are part of the Ubuntu Apache install
> No additional Ubuntu packages are required, as these modules are already part of the Apache2 package install.

Create a new configuration by copying the `/etc/apache2/sites-available/000-default.conf` to `/etc/apache2/sites-available/reverse-proxy.conf`.  This ensures you have a working backup if the configuration breaks or you wish to quickly switch back to a non-proxy configuration.

Edit `/etc/apache2/sites-available/reverse-proxy.conf` and add the following configuration inside the `VirtualHost` directive
```
     ProxyRequests Off
     ProxyPass "/" "http://localhost:8080/"
     ProxyPassReverse "/" "http://localhost:8080/"
```

`sudo a2ensite reverse-proxy` to enable the reverse-proxy configuration, which adds a symbolic link in the `/etc/apache2/sites-enabled/` directory (all configurations in this directory are included via `/etc/apache2/apache2.conf`)

Disable the other sites so that they do not over-ride the reverse proxy configuraion.  This simply removes the symbolic link from sites-enabled directory, their configuration is still in the sites-available directory.

```
sudo a2dissite scicloj
sudo a2dissite 000-default
```

`sudo systemctl restart apache2` to restart apache http server with the reverse proxy configuration


To use a number of projects or visualisation tools, update the `/etc/apache2/sites-available/reverse-proxy.conf` and add more `ProxyPass` and `ProxyReverse` directives

```
     ProxyPass "/oz" "http://localhost:8080/"
     ProxyPassReverse "/oz" "http://localhost:8080/"

     ProxyPass "/notespace" "http://localhost:8181/"
     ProxyPassReverse "/notespace" "http://localhost:8181/"
```

> #### Warning::Oz only working on `/`
> Using the reverse proxy configuration so far, Oz will only render the server page and not the views.  It is assumed that this is because of web sockets and will need to enable the mod proxy module for websockets too.
>
> References
> * https://httpd.apache.org/docs/2.4/mod/mod_proxy_wstunnel.html
> * https://www.serverlab.ca/tutorials/linux/web-servers-linux/how-to-reverse-proxy-websockets-with-apache-2-4/
> * https://websiteforstudents.com/configure-reverse-proxies-using-apache2-http-server-on-ubuntu-18-04/
