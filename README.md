# Bypass YouTube-Restrictions (Bash function).

Youtube forces to authenticate to be able to see some videos with content for adults, this is sometimes very annoying in my opinion. Not everyone has a google account or has an open session.

This authentication in google is not mandatory when videos are embedded with iframes. This function simply creates an iframe in a temporary file in / tmp / and starts the browser / opens a tab with the video.

Print the iframe in the output (you could direct it to a file to read it with a browser).
```bash
function nsfw() { 
  echo "<iframe width='560' height='315' src='https://www.youtube.com/embed/${1#*v=}' frameborder='0' allow='autoplay; encrypted-media' allowfullscreen></iframe>";
}
```

Create a temporary file with the iframe and start the firefox browser (it would work with any other browser).
```bash
function nsfw_firefox { 
  echo "<iframe width='560' height='315' src='https://www.youtube.com/embed/${1#*v=}' frameborder='0' allow='autoplay; encrypted-media' allowfullscreen></iframe>" > /tmp/${1#*v=}.htm && firefox /tmp/${1#*v=}.htm;
}
```

Add the function to any .bashrc file to have the command at any time. You simply have to pass the URL as a parameter.
```bash
nsfw_firefox https://www.youtube.com/watch?v=v8jC1NcE_2w
```
