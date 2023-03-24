#!/bin/bash
htmlfile=/var/www/html/apod.html
if  [[ $(curl -silent https://apod.nasa.gov/apod/index.html | grep ".jpg") != "" ]]
then
picture="https://apod.nasa.gov/apod/$(echo $(curl -silent https://apod.nasa.gov/apod/index.html | grep -m1 ".jpg" | sed -e 's/<a href=//g' -e 's/"//g' -e 's/>//g'))"
elif  [[ $(curl -silent https://apod.nasa.gov/apod/index.html | grep ".png") != "" ]]
then
picture="https://apod.nasa.gov/apod/$(echo $(curl -silent https://apod.nasa.gov/apod/index.html | grep -m1 ".png" | sed -e 's/<a href=//g' -e 's/"//g' -e 's/>//g'))"
elif  [[ $(curl -silent https://apod.nasa.gov/apod/index.html | grep ".mp4") != "" ]]
then
video="https://apod.nasa.gov/apod/$(echo $(curl -silent https://apod.nasa.gov/apod/index.html | grep -m1 ".mp4" | sed -e 's/<a href=//g' -e 's/"//g' -e 's/>//g'))"
fi

echo -e "<!DOCTYPE html><html lang=en><head> <link rel=stylesheet href=/style.css></head>\n<body><h1 style=margin-top:0px><a href=https://apod.nasa.gov target=_blank title='opens in new tab'>APOD</a></h1>" > $htmlfile
if [[ $picture != "" ]]
then
echo -e "<p><img alt=\"Todays Astronomy Picture of the Day from NASA\" style=max-width:100% src=$picture></p>" >> $htmlfile
else
echo -e "<p><video style=max-width:100% controls> <source src=$video type="video/mp4"> alt=\"Todays Astronomy Picture of the Day from NASA\">Your browser does not support the video tag</video></p>" >> $htmlfile
fi

if [[ $(curl -silent "https://apod.nasa.gov/apod/index.html" | grep -C 1 Copyright) = "" ]]; then
echo "No Copyright on this image :)" >> /var/www/flies/apod.html
else
echo "$(curl -silent https://apod.nasa.gov/apod/index.html | grep -C 2 Copyright | sed -e "s/<center>//" -e "s/<a href=/<a target=_blank href=/g")" >> $htmlfile
fi
echo -e "</body></html>"
