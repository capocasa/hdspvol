# hdspvol
A command-line volume tool for hammerfall sound cards on linux to replace hdspmixer

## Installation

Place the hdspvol script in your path

    # as root
    curl https://raw.githubusercontent.com/carlocapocasa/hdspvol/master/hdspvol > /usr/local/bin/hdspvol
    chmod +x /usr/local/bin/hdspvol

## Usage

Increase volume

    hdspvol inc

Decrease volume

    hdspvol dec

Mute volume

    hdspvol mute

Display current volume (0-65535)

    hdspvol show

Load volume (do this on computer startup)

    hdspvol load


## Configuration

hdspvol connects the first two buses to the first two outputs by default. To change which outputs are affected, place entries from these example configurations in `~/.config/hdspvol/rc

    # Defaults
    IN_LEFT=26
    IN_RIGHT=27
    OUT_LEFT=0
    OUT_RIGHT=1

    # Headphone output
    IN_LEFT=26
    IN_RIGHT=27
    OUT_LEFT=26
    OUT_RIGHT=27
    
    # Mono grot box on the thrid output
    IN_LEFT=26
    IN_RIGHT=27
    OUT_LEFT=2
    OUT_RIGHT=2

## Tweaks

hdspvol has large volume steps, small ones and tiny ones, to allow more fine grained control at lower volumes, while still reaching high volumes without a lot of hassle. These can also be changed in the rc file, but the defaults work great for the author.

    # Defaults
    STEP=2048
    SMALLSTEP=256
    TINYSTEP=32

Finally, if the maximum volume should be half the cards capability, or the card should never be entirely silent, minimum and maximum volume may be set.

    # Defaults
    MAX=65535
    MIN=0


## Multiple configurations

Create a symlink to hdpsvol with a name of your choice, using hdspphones as an example

    # As root
    ln -s /usr/local/bin/hdspvol /usr/local/bin/hdspvolphones

Create a configuration file as above, but use `.config/hdspohones/rc`

    mkdir -p ~/.config/hdspphones

Now you can use `hdspvol` do modify normal volume, and hdsphones to modify headphone output volume.

Create as many configurations as are needed.

## Detecting channels

To find out which channel should be used for a particular setup, install hdspscan by Klaus Schultz (included in this repository)

    # as root
    curl https://raw.githubusercontent.com/carlocapocasa/hdspscan/master/hdspscan > /usr/local/bin/hdspscan
    chmod +x /usr/local/bin/hdspscan

IMPORTANT: Dial your volume low with your hardware volume control before continuing

Now set up your cable connections to your hdsp, e.g. connect your secondary speakers to output channels 5 and 6, and configure your playback software to use the bus channels you would like. Then run

    hdspcan

After answering a series of "do you hear something" questions, hdspscan will tell you the source and destination channels to place in your hdspvol configuratoin file for this particular setup.

## Why?

Scriptability.

I have configured my computer colume controls to run hdspvol, so it is very easy to operate.

Volume controls -> main speakers
Alt+Volume controls -> headphones
Windows+Volume controls -> grotbox

## Internals

hdspvol is a more user friendly frontend for amixer. It also remembers the volume it set, so increment and decrement functions as well as returning to the previous volume at start are possible.

## Limitations

hdspvol configurations are stereo only, i.e. two channels must always connect to two other channels.

## License

hdspvol (c) 2015-2016 Carlo Capocasa. MIT license.

hdspscan (c) 2009 Klaus Schultz

Warranties: None, whatsoever, not even implied.


