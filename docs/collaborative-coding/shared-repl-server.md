# Shared REPL server

??? TODO "Create a remote serve"
    Define how to create a suitable remote server on AWS, Google, etc.

!!! WARNING "Switch off Server when done"
    Dont forget to switch the server off when not in use to avoid additional costs


## Install Clojure

Use the Clojure.org Getting Started instructions to download Clojure for Linux and run the install script.  This installs `clojure` command system wide (`/usr/local/bin/`) along with the `clj` wapper that runs a terminal REPL using `rlwrap` (TODO: check rlwrap is installed).

Use a range of community tools by installing the practicalli/clojure-deps-edn configuration (first deleting the `~/.clojure` directory if it exists - create if you run `clojure` or `clj` for the first time)

```bash
git clone https://github.com/practicalli/clojure-deps-edn.git ~/.config/clojure/
```

Created a new project on the remote server using a [Clojure project templates](https://practical.li/clojure/clojure-cli/projects/create-from-template/).  For example a simple command line application

```bash
clojure -X:project/create :template app :name practicalli/science-is-fun
```

## Run REPL with nREPL server

Start a REPL process with an nREPL server to connect a [Clojure aware editor](https://practical.li/clojure/clojure-editors/).

The REPL process can be started with a rich terminal UI if actively using the REPL prompt.  Or as a simple prompt with only command history or even as a headless process.

=== "Rich Terminal UI"
    Run a feature rich terminal REPL using the `:repl/rebel` alias from [Practicalli Clojure CLI Config](https://practical.li/clojure/clojure-cli/practicalli-config/)
    ```shell
    clojure -M:repl/rebel
    ```

=== "Headless REPL process"
    Run a non-interactive 'headless' REPL process if all the interaction is to be done via a [Clojure aware editor](https://practical.li/clojure/clojure-editors/)

    Use the `:repl/headless` alias from [Practicalli Clojure CLI Config](https://practical.li/clojure/clojure-cli/practicalli-config/)
    ```shell
    clojure -M:repl/headless
    ```

=== "Simple Built-in REPL"
    Run the REPL process with the simple prompt provided with Clojure CLI if resources are very constrained.  The `clj` wrapper requires `rlwrap` binary to be available on the operating system execution path
    ```shell
    clj
    ```


## Configure SSH connection

Generate a permissions file, `.pem` from the server (TODO: how to generate .pem files) and save it to `~/.ssh/` directory (or your preferred location).

Edit the `~/.ssh/config` file (create the file if needed) and add a host configuration for the remote server.

Add the IP address of the remote server to `HostName`.

Use the `LocalForward` for the port used by the nREPL server.

```bash
Host remote-clojure-server
  HostName 99.99.99.99
  IdentityFile ~/.ssh/remote-server.pem
  User ubuntu
  PasswordAuthentication yes
  LocalForward 1234 localhost:1234
  Port 22
```


## Start REPL with Editor support

The majority of [Clojure aware editors](https://practicalli.github.io/clojure/clojure-editors/) can connect to an external REPL using the nREPL protocol.  Emacs CIDER, VSCode Calva and NeoVim Conjure all use nREPL and the Cider middleware.

The `:middleware/cider-clj` will inject the nREPL and Cider middleware libraries.

SSH into the remote server.

Change to a Clojure project

Start the REPL using the cider middleware on the same port as defined in `LocalForward` in the SSH configuration, using the `-p` to set the port number.

```bash
clojure -M:middleware/cider-clj -p 1234
```


## Configure Emacs

Emacs can be used to connect to a running Clojure project that has been run with the nREPL and Cider middleware, e.g. `:middleware/cider-clj` from [`practicalli/clojure-deps-edn`](http://practicalli.github.io/clojure/clojure-tools/install/community-tools.html)

Edit your Emacs `~/.emacs.d/init.el` file and add the following configuration.

For Spacemacs, edit `~/.spacemacs` and add the following code to `dotspacemacs/user-config`

```emacs
(setq nrepl-use-ssh-fallback-for-remote-hosts t)
```


## NeoVim Conjure on remote server

NeoVim and Conjure are installed on the remote server using the [Practicalli install guide](https://practicalli.github.io/clojure/clojure-editors/editor-install-guides/neovim-conjure.html).

Conjure will automatically connect to a running REPL

!!! HINT "Conjure uses .nrepl-port"
    Conjure looks for the `.nrepl-port` in the root of the project.  If this file is not created when running the REPL, create the file and use the same value as `LocalForward` from the SSH configuration.


## Apache HTTPd server reverse proxy

Use a reverse proxy if you wish to expose visualizations via a browser, such as Oz or notespace.

ssh into the remote server with an account that has sudo privileges

Enable the reverse proxy module `mod_proxy_http` which has a dependency on `mod_proxy` and is also enabled automatically.

```bash
sudo a2enmod proxy_http
```

??? HINT "Modules are part of the Ubuntu Apache install"
    Proxy modules are already part of the Apache2 package install on Ubuntu, so additional package install is not required

Create a new configuration by copying the `/etc/apache2/sites-available/000-default.conf` to `/etc/apache2/sites-available/reverse-proxy.conf`.  This ensures you have a working backup if the configuration breaks or you wish to quickly switch back to a non-proxy configuration.

Edit `/etc/apache2/sites-available/reverse-proxy.conf` and add the following configuration inside the `VirtualHost` directive
```bash
     ProxyRequests Off
     ProxyPass "/" "http://localhost:8080/"
     ProxyPassReverse "/" "http://localhost:8080/"
```

`sudo a2ensite reverse-proxy` to enable the reverse-proxy configuration, which adds a symbolic link in the `/etc/apache2/sites-enabled/` directory (all configurations in this directory are included via `/etc/apache2/apache2.conf`)

Disable the other sites so that they do not over-ride the reverse proxy configuraion.  This simply removes the symbolic link from sites-enabled directory, their configuration is still in the sites-available directory.

```bash
sudo a2dissite scicloj
sudo a2dissite 000-default
```

`sudo systemctl restart apache2` to restart apache http server with the reverse proxy configuration


To use a number of projects or visualisation tools, update the `/etc/apache2/sites-available/reverse-proxy.conf` and add more `ProxyPass` and `ProxyReverse` directives

```bash
     ProxyPass "/oz" "http://localhost:8080/"
     ProxyPassReverse "/oz" "http://localhost:8080/"

     ProxyPass "/notespace" "http://localhost:8181/"
     ProxyPassReverse "/notespace" "http://localhost:8181/"
```

!!! WARNING "Oz only working on `/`"
    Using the reverse proxy configuration so far, Oz will only render the server page and not the views.  It is assumed that this is because of web sockets and will need to enable the mod proxy module for websockets too.


## References

* https://httpd.apache.org/docs/2.4/mod/mod_proxy_wstunnel.html
* https://www.serverlab.ca/tutorials/linux/web-servers-linux/how-to-reverse-proxy-websockets-with-apache-2-4/
* https://websiteforstudents.com/configure-reverse-proxies-using-apache2-http-server-on-ubuntu-18-04/
