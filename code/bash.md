# Terminal

## Homebrew

* [https://brew.sh/](https://brew.sh/)

## FFMPEG

### Making gifs

* [https://askubuntu.com/questions/648603/how-to-create-an-animated-gif-from-mp4-video-via-command-line](https://askubuntu.com/questions/648603/how-to-create-an-animated-gif-from-mp4-video-via-command-line)
* [https://medium.com/@colten\_jackson/doing-the-gif-thing-on-debian-82b9760a8483](https://medium.com/@colten\_jackson/doing-the-gif-thing-on-debian-82b9760a8483)
* [https://superuser.com/questions/556029/how-do-i-convert-a-video-to-gif-using-ffmpeg-with-reasonable-quality](https://superuser.com/questions/556029/how-do-i-convert-a-video-to-gif-using-ffmpeg-with-reasonable-quality)

```bash
ffmpeg \
  -i yourFile.mov \
  -r 15 \
  -vf scale=512:-1 \
  -ss 00:00:03 -to 00:00:06 \
  yourFile.gif
  
  #hq
  ffmpeg -i demo.mov -vf "fps=15,scale=800:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 output.gif

```

## ImageMagick

### Documentation

* [https://imagemagick.org/script/download.php#macosx](https://imagemagick.org/script/download.php#macosx)
* [https://imagemagick.org/script/convert.php](https://imagemagick.org/script/convert.php)
* [https://imagemagick.org/script/mogrify.php](https://imagemagick.org/script/mogrify.php)

### Compression

* [https://stackoverflow.com/questions/7261855/recommendation-for-compressing-jpg-files-with-imagemagick](https://stackoverflow.com/questions/7261855/recommendation-for-compressing-jpg-files-with-imagemagick)
* [Convert & save with same name](https://stackoverflow.com/questions/9992174/imagemagick-command-to-convert-and-save-with-same-name)#

```bash
#basic
magick image.jpg -strip -interlace Plane -gaussian-blur 0.05 -quality 85% -resize 75%  result.jpg

# compress all jpg in folder 
magick *.jpg -strip -interlace Plane -gaussian-blur 0.05 -quality 85% result.jpg
    
#parent folder
convert *.jpg -strip -interlace Plane -gaussian-blur 0.05 -quality 85%  -set filename:f '%t_web' ../'%[filename:f].jpg'

# into target folder in same directory
mogrify *.jpg -strip -interlace Plane -gaussian-blur 0.05 -quality 85% -path ../web *.jpg

# into target folder in parent directory
mogrify *.jpg -strip -interlace Plane -gaussian-blur 0.05 -quality 85% -path web *.jpg
```

### Change file format

* Your EPS file is in CMYK colorspace. You need to convert it to sRGB before processing it

#### PNG to JPG

{% tabs %}
{% tab title="white bg" %}
```bash
//batch 
mogrify -background white -flatten -format jpg  *.png

// single
convert Chun.png -background red -flatten  png_small.jpg

// and compress
convert moom_ref.png -format jpg -quality 85% test.jpg
convert moom_ref.png -format jpg -strip -interlace Plane -gaussian-blur 0.05 -quality 85% test.jpg



```
{% endtab %}

{% tab title="black bg" %}
```bash
//single
convert *.png -alpha off image.jpg

// batch
magick mogrify -format jpg *.png
```
{% endtab %}
{% endtabs %}

#### EPS to PNG

```
mogrify -format png -density 100 -colorspace sRGB -background transparent -units PixelsPerInch -resize 2475x3525 *.eps
```

#### Extract alpha from PNG

```
mogrify -set colorspace RGB -alpha extract -format jpg *.png
```

#### Extract alpha from white

```bash
convert test.jpg -fuzz 50%  -transparent white result.png

//batch
mogrify -fuzz 50%  -transparent white -set colorspace RGB -alpha extract -format jpg *.png


// batch add alpha from white in pngs, save to new folder
mogrify -fuzz 50%  -transparent white -set colorspace RGB -alpha extract -format jpg -path ../mask *.png
```

#### Extract color from image

```
// select red, fill rest with black
convert test.png -fill white -fuzz 10% -opaque red output.jpg

// has black outline    
convert test.png -fill black -fuzz 20% -opaque red -transparent black output.png 
convert test.png -fill black -fuzz 5% -opaque red -transparent black output.png 

mogrify -fill black -fuzz 5% -opaque red -transparent black output.jpg *png

// select red only

convert test.png -fill black -fuzz 20% -opaque #B93C3C -transparent black output.png 


```

#### Converting images to black or a fill color

```
//batch overwrite
mogrify -format jpg -fill black -background black -colorize 100%  *.jpg

```

## HtTrack

```
http://duitbetter.com/2021/04/05/shader-dev-study-01-c-arnold/,http://duitbetter.com/2021/04/12/shader-dev-study-02-sidemask-pattern/,http://duitbetter.com/2021/04/20/shader-dev-study-03-height-to-color-pattern/,http://duitbetter.com/2021/05/09/shader-dev-study-04-moom-osl-shader/

+*.gif +*.jpg +*.png +*.mp4 
```

## Ultimate Mac environment setup

### Homebrew

{% tabs %}
{% tab title="packages" %}
```bash
#homebrew
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

#packages
brew install youtube-dl
brew install python
brew install imagemagick
brew install ghostscript
brew install npm
brew install storyboarder

$ sudo easy_install pip
$ sudo pip install --upgrade pip

#cask
brew install caskroom/cask/brew-cask

#update xcode
sudo rm -rf /Library/Developer/CommandLineTools
xcode-select --install
```
{% endtab %}

{% tab title="graphical" %}
```bash
#utility
    brew cask install google-chrome
    brew cask install obs
    brew cask install streamlabs-obs
    brew cask install clipgrab
    brew cask install spotify
    brew cask install handbrake
    brew cask install vlc
    brew cask install easyfind
    brew cask install station
    brew cask install sync
    brew cask google-backup-and-sync
    brew cask install the-unarchiver
    brew cask install zoomus
    brew cask install alfred

#code
    brew cask install atom
    brew cask install processing

# design
    brew cask install figma
    brew cask install blender
    brew cask install adobe-creative-cloud
    brew cask install zxpinstaller
```
{% endtab %}
{% endtabs %}

* xcode: [https://stackoverflow.com/questions/34617452/how-to-update-xcode-from-command-line](https://stackoverflow.com/questions/34617452/how-to-update-xcode-from-command-line)
* [Installing packages from terminal](https://www.howtogeek.com/211541/homebrew-for-os-x-easily-installs-desktop-apps-and-terminal-utilities/)

### Atom setup &#x20;

```bash
#Go to Menu > Install Shell Commands
#run below
apm install adobe-script-runner atom-beautify prettier-atom atom-spotify2 
atom-transpose case-keep-replace change-case copy-path duplicate-line-or-selection
editorconfig file-icons git-plus highlight-selected local-history project-manager 
related set-syntax sort-lines sublime-style-column-selection tab-foldername-index 
toggle-quotes atom-wrap-in-tag atom-ternjs autoclose-html 
autocomplete-modules color-picker docblockr emmet emmet-jsx-css-modules 
es6-javascript js-hyperclick hyperclick pigmentstree-view-copy-relative-path
lodash-snippets language-babel atom-jest-snippets one-dark-ui dracula-theme

##react-es7-snippets sync-settings  linter-eslint 

```

### Get all DMG

```bash
#utility
    open https://www.pureref.com/freedownload.php?build=OSX64.dmg&version=1.11.1&downloadKey=kwshPqIAWUNsGVwJYCjKag%3D%3D
    #utorrent
    #Microsoft Office
    open https://login.microsoftonline.com/?whr=scad.edu
    open https://depts.scad.edu/coronavirus/academic-software

# optimize
    open https://apps.apple.com/us/app/magnet/id441258766?mt=12
    
#creative 
     open https://www.blackmagicdesign.com/products/davinciresolve/
```

### Change screenshot directory

```
cd ~/desktop
mkdir screenshots

defaults write com.apple.screencapture location ~/desktop/screenshots
defaults write com.apple.screencapture type -string "png"
```

### [Disable Drop-shadow screenshots](https://www.dessol.com/blog/disable-drop-shadow-mac-osx-window-screenshots/)

```
defaults write com.apple.screencapture disable-shadow -bool true
killall SystemUIServer
```

