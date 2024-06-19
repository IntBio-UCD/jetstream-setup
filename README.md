# jetstream-setup

see `setup.md` for software installations

## create an instance

First register at [https://access-ci.org/](https://access-ci.org/), then ask Julin to add you to this allocation.

Go to the [jetstream portal](https://jetstream2.exosphere.app/)

If the IntBio allocation is not showing, click on "add allocation" and then authenticate and add it.

If you don't already have an instance, create one:
* Click on `Create > Instance`
* If you want to use my image with many programs and R packages already installed, select `By Image` and then search for "IntBio" (alternatively, select the base image of your choice)
* Click `Create Instance`
* Enter an Instance name.  Please include your name in the instance name
* Choose your size.  Please use the smallest size that can accomplish what you need.  Note that you can resize later.
* You probably want a Custom Disk Size (maybe 100GB; I have shared file systems (see below) for large files)
* Click to `Enable Web Desktop`

## accesss your instance

* Click on you instance.  Wait for it to finish building (takes 3-5 minutes)
* Once the satus is "ready" you can access your instance by:
  + Click on "Web Desktop" to open a GUI viewer in your web browser.  Cut-and-paste works better for me in Chrome than in Safari, but there is probably some Safari setting that can be changed.  Web desktop sessions are persistent even if you close the tab or quite your browser.
  + You can click on "Web Shell" for a text interface through your browser, but if I want a text session then I strongly prefer using SSH
  + You can use SSH from your terminal.  The ip address is shown on the Jetstream portal.  Click on `Passphrase` to get your password
    + You may want to add your ssh public key, then you won't need a password (ask Julin for help)
    + Remember to start a [Screen](https://jnmaloof.github.io/BIS180L_web/2024/05/17/screenGuide/) or [tmux](https://github.com/tmux/tmux/wiki) session if you want your session to persist when closing your laptop, etc.
   
## personalization

For github, at the terminal set your email and name (replace info in brackets below)
```
git config --global user.email "[YOU]@ucdavis.edu"
git config --global user.name "[YOUR NAME]"
```
   
## IMPORTANT Shelve your Instance!

__SHELVE YOUR INSTANCE WHEN YOU AREN'T USING IT.  GO TO THE `ACTIONS` MENU ON JETSTREAM AND SELECT `SHELVE`__

##  Installed Programs

See [setup](https://github.com/IntBio-UCD/jetstream-setup/blob/main/setup.md)

Note that igv, minimap2, STAR, seqkit, and busco are in the conda envrioment `sequencing` (type `conda activate sequencing` to access these)

## Storage

Raw data is in `/raw_seq_data` and is mounted read only

You can use `/analyzed_data` both for your working space and finalized analyses.  Use a folder with your username for work in progress, and them move to `finalized_analyses` when you are done.

