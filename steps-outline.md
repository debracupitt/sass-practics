#1.5

#1.6
##Speed up development with Grunt Watch
How to watch SCSS files and compile them to CSS whenever you edit them.
Go to the Terminal, and run:

`npm install grunt-contrib-watch - -save-dev`

As you can tell from the name having contrib, this plugin is maintained by the Grunt team.

Once that is installed go to Text editor and edit the Grunt file. You should add lines to make it look like this:

`

      const sass = require("node-sass");
      module.exports = function(grunt) {
        grunt.initConfig({
          sass: {
            options: {
              implementation: sass,
              outputStyle: "expanded"
            },
            dist: {
              files: [{
                expand: true,
                cwd: "assets/sass/",
                src: "**/*.scss",
                dest: "assets/css/",
                ext: ".css"
              }]
            }
          },
          watch: {
            files: "assets/sass/\*_/_.scss",
            tasks: "sass"
          }
        });

      grunt.loadNpmTasks("grunt-sass");
      grunt.loadNpmTasks("grunt-contrib-watch");

      grunt.registerTask("default", ["sass", "watch"]);

    };

`
For the properties for this you can view them on the grunt-contrib-watch page on github.com.

So this says whenever any of the SCSS files in this folder or subfolders are changed run this sass task. You have also Now made `watch` a default Grunt task.

To do run the watch command in the terminal, run:
`grunt watch`

The default alias name is special for Grunt in that it means you can simply run `grunt` from the command line and the default task will run. Save the file and test it in the Terminal. You can then press control C again to stop that process.

Your development setup with Grunt Watch will now make it easy for you and other developers to quickly get started developing Sass.

#1.7

The original syntax of Sass includes no curly braces, no semicolons and uses indentation to delimit block of styles. It's more concise, but it does not look like CSS.

SCSS looks exactly like CSS. You can take your CSS files, move them to your Sass folder, change the extension to SCSS and you have valid SCSS. So, for your first commit of an SCSS file, you can do just that.

One feature of Sass that is pretty powerful is the ability to nest your rules. The Ruby version of Sass actually comes with a commandline tool to convert your CSS to SCSS and automatically add nesting to the SCSS files. (I’m using the lib version of sass with node-sass). That does not exist in LibSass.

This online tool provides the same functionality: css2sass.herokuapp.com.

Just don't blindly use the tool though as although it will generate the same styles for you, it may alter your selectors a bit. For example, if you have multiple selectors of the same block of styles, and then one of those selectors is used separately, as we do in our CSS file with the sub and sup selectors here, it will duplicate each selector in the multi-selector block style and add the additional styles instead of maintaining the multiple selectors.

After you run the tool, it may require some manual adjusting to get it where you like it. If you have a large amount of CSS you're converting, you may want to skip this automated step entirely and just add nesting as you wish later on manually.
e. g. Another spot this happens is down below here. So we have this webkit appearance button and cursor pointer and a couple of spots here that are all in the SCSS covered by this one line of selector. So there's four selectors there. We can just copy this from the CSS and paste it in the SCSS. Just below that, we see the border and padding are set in multiple spots here, and that selector is right here so I'll go ahead and I will copy that.

Also, there's the potential for comments to end up out of placeIf we take a look back at your original CSS and search, you can see where it is meant to be.

When you're writing new Sass code, it's easy to get carried away with nesting and go many levels deep. This typically results in bloated, unnecessary CSS. So it's best to follow what's known as the inception rule, which was coined on this article on the Sass way. The rule states that you should never nest more than four levels deep.

Additionally, now that you're using nesting to create selectors, you're generating selectors for browsers to use that don't exist in your actual Sass source code. So if you're used to inspecting the element with the browser's developer tools, copying the selector and searching for it in your code base, your searches will come up empty if the selector was generated due to nesting. This sways some developers away from using nesting at all in Sass. I personally still enjoy the organization and reduced typing nesting affords, and with the debugging techniques that Sass offers, you can be working just as fast as you were with vanilla CSS.
