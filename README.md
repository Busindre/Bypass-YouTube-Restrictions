# Bypass YouTube-Restrictions (Bash function / youtube-dl).

Youtube requires you to authenticate to be able to see some videos with rated content, This may be very annoying. Not everyone has a Google account or has an open session.

This google authentication was not mandatory when videos are embedded inside iframes, but that changed at the end of 2020. This function simply creates an iframe in a temporary file in /tmp and starts the browser or opens a tab with the selected video. But due to the mandatory login, this time using one of the alternative frontend services for youtube [Invidious Instances](https://docs.invidious.io/instances/). The example uses a service from this list, but you can adapt it to your needs.



## Browser

Print the iframe in the output (you could direct it to a file to read it with a browser).
```bash
function nsfw() { 
  echo "<iframe width='560' height='315' src='https://vid.puffyan.us/embed/${1#*v=}' frameborder='0' allow='autoplay; encrypted-media' allowfullscreen></iframe>";
}
```

Create a temporary file with the iframe and start the Firefox browser (it would work with any other browser).
```bash
function nsfw_firefox() { 
  echo "<iframe width='560' height='315' src='https://vid.puffyan.us/embed/${1#*v=}' frameborder='0' allow='autoplay; encrypted-media' allowfullscreen></iframe>" > /tmp/${1#*v=}.htm && firefox /tmp/${1#*v=}.htm;
}
```

Add the function to any .bashrc file to have the command available whenever you need it. You simply have to pass the desired youtube URL as a parameter.
```
nsfw_firefox https://www.youtube.com/watch?v=v8jC1NcE_2w
```

## youtube-dl / mplayer / VLC

youtube-dl sends the youtube video (+ audio ;D) to the standard input and the player receives it to start playing it.

```bash
# mplayer
function nsfw_terminal () { youtube-dl --quiet -i -o - "$1" | mplayer -really-quiet -; }

# VLC
function nsfw_terminal () { youtube-dl --quiet -i -o - "$1" | vlc -; }
```

Add the bash-function to any .bashrc file to have the command available whenever you need it. You simply have to pass the desired youtube URL as a parameter.
```
nsfw_terminal https://www.youtube.com/watch?v=fDYPu20pnBI
```
