
**Please note this repository host code of https://github.com/FortyNorthSecurity/EyeWitness before https://github.com/FortyNorthSecurity/EyeWitness/commit/b7d8a4698c13c103eb12cbbdcb6afe3246a934cf commit, as headless firefox is very slow compared to selenium. Although selenium is no longer maintained but still works great.**

EyeWitness
======

EyeWitness is designed to take screenshots of websites, RDP services, and open VNC servers, provide some server header info, and identify default credentials if possible.

EyeWitness is designed to run on Kali Linux. It will auto detect the file you give it with the -f flag as either being a text file with URLs on each new line, nmap xml output, or nessus xml output.  The --timeout flag is completely optional, and lets you provide the max time to wait when trying to render and screenshot a web page.

A complete usage guide which documents EyeWitness features and its typical use cases is available here - https://www.christophertruncer.com/eyewitness-usage-guide/

###### Supported Linux Distros:
* Kali Linux
* Debian 7+ (at least stable, looking into testing) (Thanks to @themightyshiv)


**E-Mail:** EyeWitness [@] christophertruncer [dot] com

### Setup:
1. Navigate into the setup directory
2. Run the setup.sh script

### Usage:
```bash
./EyeWitness.py -f filename --timeout optionaltimeout --open (Optional)
```

### Examples:
```bash
./EyeWitness -f urls.txt --web

./EyeWitness -x urls.xml --timeout 8 --headless

./EyeWitness -f rdp.txt --rdp
```

### Docker
Now you can execute EyeWitness in a docker container and prevent you from install unnecessary dependencies in your host machine.

**Note:** execute *docker run* with the folder path in the host which hold your results (**/path/to/results**)  
**Note2:** in case you want to scan urls from a file, make sure you put it in the volume folder (if you put *urls.txt* in */path/to/results*, then the argument should be *-f /tmp/EyeWitness/urls.txt*)

##### Usage
```bash
docker build --build-arg user=$USER --tag eyewitness .
docker run \
    --rm \
    -it \
    -e DISPLAY=$DISPLAY \                   # optional flag in order to use vnc protocol
    -v /tmp/.X11-unix:/tmp/.X11-unix \      # optional flag in order to use vnc protocol
    -v /path/to/results:/tmp/EyeWitness \
    eyewitness \
    EyeWitness_flags_and_input
```

##### Example #1 - headless capturing
```bash
docker run \
    --rm \
    -it \
    -v ~/EyeWitness:/tmp/EyeWitness \
    eyewitness \
    --single http://www.google.com \
    --headless
```

##### Example #2 - vnc capturing
```bash
docker run \
    --rm \
    -it \
    -e DISPLAY=$DISPLAY \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    -v ~/EyeWitness:/tmp/EyeWitness \
    eyewitness \
    -f /tmp/EyeWitness/urls.txt \
    --vnc
```

###### Call to Action:
I'd love for EyeWitness to identify more default credentials of various web applications.  
As you find a device which utilizes default credentials, please e-mail me the source code of the index page and the default creds so I can add it in to EyeWitness!
