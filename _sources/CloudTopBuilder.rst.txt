CloudTopBuilder
***************

The CloudTopBuilder is a python 3 code which reads a yaml description of a desired docker image and creates a corresponding docker build file. Once the build file is produced, it is an input to the normal docker build command.  The tags supported by the CloudTopBuilder are described below, but please see the examples in the CloudTopBuilder repository (https://github.com/helxplatform/CloudTopSDK.git) and in the Examples section of this documentation.

*Usage*
* The CloudTopBuilder requires only one argument, which specifies the yaml file. It is important that the executable be called in the same directory that includes the script files specifed in the yaml. To clone the repo, and try the napari example, execute these commands::

   cd yourRepoDir
   git clone https://github.com/helxplatform/CloudTopSDK.git
   cd CloudTopSDK/example/napari
   ../../CloudTopBuilder.py napari.yml

This will produce a Docker.napari file and a "generated" directory that can be deleted once the docker image has been built.

*output*

* The output tag specifies the name of the docker build file to be created.

*run*

The run tag instructs the CloudTopBuilder to emit instructions in the output file that will either run
commands at docker build time or execute a script at build time. The run tag has 2 sub tags, both of which are yaml arrays, meaning they can have more than one value:

   * commands: The commands tag specifies commands to be inserted directly into the docker build file. If, for example, you need a directory in the final image you can add it by putting a mkdir command in the commands stanza.

   * scripts: The scripts tag specifies executables that should be run during the docker build process. This can be used for tasks such as getting software with wget, installing libraries using apt or cloning git repositories.

*shortcuts*

The shortcuts tag allows you to specify an array of shortcuts that will appear on the desktop of your CloudTop based image.  This shortcut will launch the specified program when clicked. Each shortcut has a title and within the name are three additional tags that specify the attributes of the shortcut. These are

   * icon:  This is the png file that will be used to represent for the shortcut. This is optional: if you omit it a default icon will be used
   * exec: This is the program, including arguments to be launched when the icon is selected.
   * name: This is the text to be displayed below the icon on the desktop.  This is optional. If it is not provided, the title of the shortcut will be used as the text.
