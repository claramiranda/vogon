# Vogon

Vogon combines a video creative, a data table(Feed) and a layout specification,
generating a copy of the video creative combined with each line of the data
table according to the layout specification.

The data can contain text, images and videos. The specification determines the timing,
position and font definitions for each piece of text, video and image,
referencing data fields through their names. Fixed text can also be
used in the layout specification.

The generated videos are (optionally) uploaded to a Youtube channel,
and a Google Ads Campaign specification file is generated to be imported in Google Ads
for Video, creating keyword/audience/interest/geo-targeted campaigns for each of the videos.

This is not an official Google product.

This tutorial will help you get Vogon up and running on your own infrastructure.

It goes as follows:

* 1 - Installing the Solution
* 2 - Accessing the Web-App
* 3 - User Manual
* 4 - Frequently Asked Questions (FAQ)

## 1 - Installing the Solution

We have main steps here:

0. Install Vogon
0. Get APIs Access

**Installation** should cover following packages:

* Install *ffmpeg* and *imagemagick*
* Install GIT
* Install *Python3* and *pip3*
* Install Python libs with pip
  * google-api-python-client
  * oauth2client
  * bottle
  * http.client
  * httplib2
* Download Vogon codeAfter that

**APIS** should be:
* YouTube Data API V3
* Google SHEETS

### 1.1 - Installing Vogon
We got two flavors here:

* Linux (Debian/Ubuntu)
* Mac OS X

But have fun installing where ever you may seen fit :)

#### 1.1.1 - Linux install (Debian/Ubuntu)
Depending on the distro, the set of commands to install all required
dependencies shall look like this:

```bash
# install  ffmpeg * imagemagik
sudo apt-get install ffmpeg;
sudo apt-get install imagemagick;

# install GIT
sudo apt-get install git;

# install python3 and pip3
sudo apt-get -y install python3-pip;

# install python libs
pip3 install --upgrade google-api-python-client;
pip3 install --upgrade oauth2client;
pip3 install --upgrade bottle;
pip3 install --upgrade retry;
pip3 install --upgrade http.client;
pip3 install --upgrade httplib2;

# Download Vogon code
cd {YOUR_VOGON_APP_DIR};
git clone https://github.com/google/vogon.git
```


#### 1.1.2 - Mac OS X Install
Depending on the OS X version, the set of commands to install all required
dependencies shall look like this:

```bash
# install home brew
xcode-select --install
sudo easy_install pip
sudo pip install --upgrade pip
ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"

# install  ffmpeg * imagemagik
brew install ffmpeg;
brew install imagemagick;

# install GIT
brew install git;

# install python3 and pip3
brew install python
brew install python3

# install python libs
pip3 install --upgrade google-api-python-client;
pip3 install --upgrade oauth2client;
pip3 install --upgrade bottle;
pip3 install --upgrade retry;
pip3 install --upgrade http.client;
pip3 install --upgrade httplib2;

# Download Vogon code
cd {YOUR_VOGON_APP_DIR};
git clone https://github.com/google/vogon.git
```

### 1.2 - Get API Access
Vogon uses two main APIs to run smoothly:

* YouTube API: upload generated videos to YouTube.
* Google Sheets: Manipulate Vogon on a web interface.

#### 1.2.1 - YouTube DATA V3 API
This API is used to upload Videos generated by Vogon to Youtube, making it possible
to run ads on them.

0. Enable YouTube DATA V3 API API
   0. Go to the [YT data API Console](https://console.developers.google.com/apis/library/youtube.googleapis.com)
     and enable the api.
   0. Visit the [Enabled APIs page](https://console.developers.google.com/apis/enabled).
     In the list of APIs, make sure the status is ON for the YouTube Data API v3.
0. Create a "SERVER client secret"
   [create oAuth client type OTHER](https://console.developers.google.com/apis/credentials/oauthclient/)
0. Download "SERVER client secret" json file
0. Move downloaded file to app credentials folder as **"webserver_client_secret.json"**.
0. If you intend to upload more than 3 videos a day to YouTube, you should request more quota for YouTube API v3. Each Vogon upload costs around 1600 quotas, as fo data of publication of this readme file.


#### 1.2.1 - Google Sheets API
This API is used to read and update Vogon feed.

0. Enable Google Sheets API
   0. Go to the [Sheets API Console](https://console.developers.google.com/apis/library/sheets.googleapis.com)
     and enable the api.
   0. Visit the [Enabled APIs page](https://console.developers.google.com/apis/enabled).
     In the list of APIs, make sure the status is ON for the Sheets API.
0. Create an "WEB APPLICATION secret":
   [create oAuth client of type WEB_APPLICATION](https://console.developers.google.com/apis/credentials/oauthclient/)
0. Download "WEB_APPLICATION client" json file
0. Move downloaded file to app credentials folder as **"oauth_2_client_secret.json"**

#### 1.2.3 - When you are done...

Your app credentials folder  should look something like this

* .git
* base_project
   * ...
* credentials
   * .keep
   * **webserver_client_secret.json**
   * **oauth_2_client_secret.json**
* ...


## 2 - Accessing the Web-App

* Start the web app (Make sure port 8080 is free)

```bash
cd {YOUR_VOGON_APP_DIR};
python3 server.py --debug
```

* Open solution on a browser: [http://localhost:8080](http://localhost:8080)

## 3 - User Manual
Check [User Manual  PDF](User_Manual.pdf) :)

## 4 - FAQ

1. **What image formats are accepted**?

In a nutshell: **jpg, gif & png**.
Animated or not, with transparent background or
not.

2. **Does Vogon accept animated gifs**?

Yes! you have to set the animated gif overlay FADE-IN and
FADE-OUT to zero "0" so that Vogon can understand that your
gif might be animated.

3. **Does Vogon accepts images with transparent background/
alpha channel**?

Yes. Just add them as any other image.

4. **Does Vogon accepts different audio tracks for each variation**?

Kinda... You can add the base video with a MUTED
soundtrack(it has to have an audio track) and add other
video overlays with the audio track you want for each
variation.

5. **Can i put an image or a video on top of a text overlay**?

Nope... Text overlays always stay on top of image or video overlays.
