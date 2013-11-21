How to create a Playground for Teamwork
======

Creating a Teamwork Playground is really easy. After you completed your content for your Playground you need to edit two files and create a merge request on Github, then it will be published instantly. 

Clone [Koding's Teamwork Repository](https://github.com/koding/Teamwork) and go to **Playgrounds** folder and open up **manifest.json**.

In manifest.json, you will see lots of Playground config. Add your own config here. Below you can see a sample of Playground config. 

	{
	   "name": "Facebook",
	   "manifestUrl": "https://raw.github.com/koding/Teamwork/master/Playgrounds/Facebook.json",
	   "description": "Facebook Playground",
	   "icon": "https://teamworkcontent.s3.amazonaws.com/covers/facebook.png"
	 }


Here is the details of config. 

* **name** It's name of your Playground. It must be unique.
* **manifestUrl** Url of the your Playground's manifest file. We will cover the manifest file content.
* **description** A few words about of your Playground.
* **icon** Cover icon of your Playground. It must be 240px by 240px. It will be used on the Teamwork Playgrounds Modal, [see this screenshot](http://d.pr/i/7oI4).
	
Now it's time to create your Playground's **manifest** file. This file will be used to customize Teamwork for your Playground and let you easily change look and feel and the functionality.

A complete manifest file is exactly like that. [Click here to see it's on Github](https://github.com/koding/Teamwork/blob/master/Playgrounds/Bootstrap.json)

	{
	  "name": "AngularJS",
	  "version": "1.2.0",
	  "styling": {
	    "textColor": "#FFF",
	    "textShadowColor": "none",
	    "borderColor": "#e52a3a",
	    "bgColor": "#e52a3a",
	    "bgImage": "https://teamworkcontent.s3.amazonaws.com/icons/angularjs.png"
	  },
	  "content": {
	    "type": "zip",
	    "url": "https://teamworkcontent.s3.amazonaws.com/zipfiles/AngularJS.zip"
	  },
	  "run": {
	    "handler": "preview",
	    "command": "https://$USERNAME.kd.io/Teamwork/AngularJS"
	  },
	  "initialState": {
	    "preview": {
	      "url": "https://$USERNAME.kd.io/Teamwork/AngularJS"
	    },
	    "editor": {
	      "files": [ "./index.html" ]
	    }
	  }
	}
	
Here is the details of this file.

**name** Name of your Playground. Keep it short and meaningful.

**version** Version of your Playground. If you make a Playground for a framework like AngularJS then you may want to use it's version number as your Playground's version. Otherwise it's a good idea to start your version number by ```0.1```. Let's say, you add new examples to your Playground and want to publish latest content, you need to update version number and Teamwork users will be prompted again to download latest content.

**styling** Styling options will be applied to Teamwork's header. With this styling options, you can change text color, background color and even the logo of Teamwork and make your Playground unique.

* **textColor** Color of the title. Default is `#4c4c4c`.
* **textShadowColor** Pass a color if you want to add shadow of your title, otherwise pass none. Default is none.
* **borderColor** Teamwork header has `3px solid #c7c7c7` border at the bottom. Pass a color to override it.
* **bgColor** Background color of the header.
* **bgImage** Logo of your Playground. It must be 37px by 37px. Otherwise it will be forced to that size. Default is Teamwork Logo.

**content** Let Teamwork know where is your Playground's content. ```content``` config requires two property, ```type``` and ```url```. Currently only supported content type is ```zip```. So your content must be zipped and put a publicly available location. 

**run** With this config option, you can execute a command on Terminal or open a web page on Teamwork's Previewer. ```run``` config requires 2 propery, ```handler``` and ```command```.

* **handler** Handler defines which Teamwork pane will be visible and do something when user clicked to Run button. It should be ```terminal``` or ```preview`` `.
* **command** The command that will be run on Terminal or opened by Preview. We give you some placeholders to deal with the active state of Teamwork. 
	* **$ACTIVE_FILE_PATH** This placeholder can be used with Terminal. If your command includes this placeholder, it will be replaced by the active file's path on the editor.
	* **$USERNAME** This placeholder can be used with Preview or Terminal. If your command includes this placeholder, it will be replaced by the Teamwork's session owner username.

**initialState** This config will be used to decorate the Teamwork panes after it became ready. For example you can open a web page or open your default files to editor when you Playground opened.
	* **preview** Define a ```preview``` object and ```url``` property in it to open a web page. You can use some placeholders inside of url. See the documentation for **command**.
	* **editor** Define a ```editor``` object and ```files``` property in it to open the files you want.  ```files``` must be an array that contains file paths. It must start with ```./``` which defines the root of your zip file.

**prerequisite** This config will be used to check your Playground is ready if you have something to do before it opened. For example, each time user has opened the Wordpress Playground, we have to check a database named wordpress. ```prerequisite``` config requires two parameters, ```type``` and ```command```. Currently only implemented pre-requisite type is ```sh```. So this means your command will be run on Terminal before user start to interact with your Playground.
