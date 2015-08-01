[ ![Codeship Status for
inspicorp_lightning/lightning-client](https://codeship.io/projects/207c8650-ed30-0131-838b-4216c01ccc74/status)](https://codeship.io/projects/26654)


# README #
Client code for Inspicorp's Lightning project 

### Quick start ###

If you do not have grunt installed:

```
#!bash

sudo npm install -g grunt-cli
```

If you do not have compass-sass installed:

```
#!bash

sudo apt-get install ruby   # If you dont have gem installed
sudo gem install compass
```

Install node_modules and bower_components:


```
#!shell

sudo npm install
bower install
```


### Build, compile and deploy ###

To compile for development, type:


```
#!bash

grunt serve
```


To compile for deployment, type:


```
#!bash

grunt serve:dist
```

This command creates a 'dist' folder in the working directory.  You can use the content in this 'dist' folder to deploy to Heroku.


### Who do I talk to? ###

* Phi Dang (danghoaiphi@gmail.com)

### Test ###

If you dont have PhantomJS installed, follow this link:
http://phantomjs.org/download.html

To test, run:
```
#!bash

grunt test:client
```

# Image Uploader #

Since image uploader (IU) is parently customized directive, it is developed for the most cases of use:  

```
<button class="btn btn-primary btn-lg" iu iu-result="result($err, $data)">Single</button>
```

The above code will show up a button which will open up an IU modal on click  

### Usage ###

Below are directives using in the main view:  

Directive | Definition
--- | ---
``iu`` | Set up IU as an attribute inside an element, **is compulsory** | 
``iuSingle`` | Control the IU to upload only 01 image at a time, without this (default) is **multiple** 
``iuCropEnable`` | Enable user to crop the image in case of use, default is **false** 
``iuCropConfig`` | Developer places config here, **only takes effect when crop has been enabled** 
``iuResult`` | The callback return function for developer to use

Basically, the most simple IU contains at least 2 directive: ```iu``` and ```iuResult``` to initalize and take the result from the directive  

For configuration, ```iuCropConfig``` takes an **object** as value, the following is current available config:  

Property | Default | Definition | Require
--- | --- | --- | ---
``auto`` | false | Enable IU to enter crop mode automatically when user enter preview mode (view a specific image) | 
``aspectRatio`` | null | Set the crop to be in a specific ratio, e.g: **4/3**, **16/9**, **1**. In default the crop box will be free sizing
``resize`` | false | Set the resize sizing, takes effect after aspectRatio done. E.g: **[400,300]**, **[800,600]** | ```aspectRatio```
``quality`` | 1 | Set the quality of the image after crop
``setSelect`` | 0 | Set the initial select zone when enter crop mode. Takes an array as **[x1,y1,x2,y2]** for custom zone, **0** for empty zone and **undefined** for no select zone | must be in same ratio as ```aspectRatio```

So in full option, it would look like:  

```<button class="btn btn-primary btn-lg" iu iu-single iu-crop-enable iu-crop-config="cropConfig" iu-result="result($err, $data)">Single</button>```

```
$scope.cropConfig = {
	auto: true,
	aspectRatio: 4/3,
	resize: [400,300],
	quality: 0.5,
	setSelect: [0,0,400,300]
};
```

### View customization ###

You can have a look in the modal view: ```single.html``` or ```multiple.html```

For furthur information, below are supporting directive used in modal view: 

Directive | Definition | Example
--- | --- | ---
```iuBtn``` | Add click event to open file browsing use to upload  | ```<button iu-btn>Add</button>```
```iuDrop``` | Add drag and drop file event use to upload | ```<div iu-drop ></div>```
```iuUrlBtn``` | Add event controller for upload via url | ```<button type="submit" iu-url-btn>Upload</button>```
```iuUrlAdd``` | Add more url input when multiple uploading, maximum of 3 | ```<button iu-url-add>Add more URL</button>```
```iuCrop``` | Add the crop controller, is **essential** when enable crop | ```<div iu-crop>...</div>```
```iuGalleryImg``` | Add gallery control for better view when multiple uploading | ```<div iu-gallery-img>...</div>```
```iuCenter``` | Centerize the modal in most cases | ```<div class="modal" iu-center>...</div>```
