# Script - Extension - Properties Panel
Hello Everyone, This is Prabhu from Code Loop. Welcome to another video on Qliksense Extension Development Series - Property Panel Basics. 

change slide

In the previous video, we have created a basic table using Qliksense Extension. we have formatted the table with Bootstrap Library. And also we saw how to apply selection on selecting a value in the table

change slide

In this video, I’m going to show you how to use custom properties to choose 


- a theme for the table
- changing cell alignment of each column
- Show or hide column based on a condition

to achieve this we are going to use custom properties in Qliksense Extension. There are a lot of components available to define a custom property. Like dropdown, Textbox, Button, Switch, slider, color picker etc.

Here for theme selection, it would be appropriate to use a drop-down component. Because we are going to provide a list of themes to select from.

For changing the cell alignment we can provide either a drop-down option because it is also a set of defined values like left, center and right. or We can show a grouped button to represent these three options.

For show and hide, we need to provide an option to enter a conditional expression to decide whether to show the column or not.

Apart from these components, there are a lot of components available in Qliksense extension. You can refer this documentation for more info. 

[https://help.qlik.com/en-US/sense-developer/April2020/Subsystems/Extensions/Content/Sense_Extensions/Howtos/working-with-custom-properties.htm](https://help.qlik.com/en-US/sense-developer/April2020/Subsystems/Extensions/Content/Sense_Extensions/Howtos/working-with-custom-properties.htm)

The implementation method is same for all the components. So I’m going to show you how to use the drop-down component, button component and Expression component.

Go to slide Change Slide

Without wasting time let’s jump on to the code and add these components.

_ End of part 1

First of all, We need to decide where exactly we need this custom property should come. If you look at the property panel, we have different sections for dimensions, measures, sorting and settings. You can add a custom property under any of these sections or you can create a new section and add it.

For choosing the themes it would be appropriate to add this under the settings.

So in the script file, add items under settings. 


    items: {
    // add all items
    }

it is an object. Within this object, we need to add all the custom properties.

Let’s add a property for theme selection, Let’s Name this as 'theme'. 


    items: {
      //For Theme selection
      themes:{
        
      }
    } 

You can give any name here. Just make sure it is relevant to the property that we are defining.

For any custom property two things are must, type and label.


    items: {
      //For Theme selection
      themes:{
        type: "",
        label: ""
      }
    } 

Type will decide the data type of the property. Like string or integer.

Label helps the user to understand the purpose of the property. So give a meaningful name here.


    items: {
      //For Theme selection
      themes:{
        type: "integer",
        label: "Choose a theme"
      }
    } 

For themes, let's give the type as integer and label as Choose a theme.

Next we need to choose the component type. At this stage, if you save the script and check the property panel in the Qliksense. 

It will show the input text box. So the default component is a text box.

Now let’s define the component in the script as `dropdown`. 


    items: {
      //For Theme selection
      themes:{
        type: "integer",
        label: "Choose a theme",
        component: "dropdown"
      }
    } 

After this we need add one more important property which is reference. It is a unique name of the property. We are going to access this property or refer this property in the script using this name .


    items: {
      //For Theme selection
      themes:{
        type: "integer",
        label: "Choose a theme",
        component: "dropdown",
        ref: "custom.theme"
      }
    } 

I’m going to give the name as custom.theme. You can give any name here without space.

So we have defined the theme property. But it is a `dropdown` property so we have to define the options that should come under this dropdown. Otherwise it will show an empty dropdown.


    items: {
      //For Theme selection
      themes:{
        type: "integer",
        label: "Choose a theme",
        component: "dropdown",
        options: []
      }
    } 

For this we need add ‘options:' . it is an array. Within this array we need add an object again. Which will have two values a value and a label.


    items: {
      //For Theme selection
      themes:{
        type: "integer",
        label: "Choose a theme",
        component: "dropdown",
        options: [{
                value: 1,
                label: "Theme 1"
        }]
      }
    } 

If you see here in the type we have defined it as an integer. so the value also should be an integer.
 The label is a string which will be displayed in the dropdown.
 

     items: {
      //For Theme selection
      themes:{
        type: "integer",
        label: "Choose a theme",
        component: "dropdown",
        options: [{
                value: 1,
                label: "Theme 1"
        },
        {
                value: 2,
                label: "Theme 2"
        }],
        defaultValue: 1
      }
    } 
    

I’m going to add one more value here. 

And also the last property which is a default value 1 the first theme.
 
That’s it. We have defined the dropdown component. Let’s check that in the dashboard.
 
So if you make any changes in the extension property, it is always a best practice to re add the extension. So that we won’t get any issues.

Let’s do that. Let’s refresh the page and re add the extension.

If you check the output it is showing the dropdown with two values and the first value is selected by default.

Now we need to see how to read this in the script. I have already added the console.log statement in the script to check the layout property.

Check that console log in the developer tools. Expand the option, under layout, you will be able to see “custom” property. Under this we can see theme. and its value is 1.

It got this name custom and theme because we mentioned it in the dropdown component definition. Because we added this reference as custom.theme., it automatically moved that theme under custom as JSON. In this way you can group multiple properties under one common name.

So just right click on the property and select copy property path. And go to the script.

Here i’m going to create a variable to store this value. Say 'ThemeIndex’ equal to ‘layout.custom.theme’.


    var themeindex = layout.custom.theme

We have already seen how to use the bootstrap class to customize a table design. Now we are going to do the same. But this time it will be a parameterized one. The theme class will be selected based on this ‘ThemeIndex’ variable.

Let’s see how many styles are there in bootstrap for tables.


https://getbootstrap.com/docs/4.0/content/tables/


Refer the bootstrap documentation for this. If you look at here we have a design here with dark background. For this we need to use table-dark class.  Similarly for each design we just need to change the class name.

So i’m going to create an array with all the class names.


    var listThemes = [
      'table-dark',
      'table-striped',
      'table-striped table-dark',
      'table-bordered',
      'table-bordered table-dark',
      'table-hover',
      'table-hover table-dark',
      'table-sm'
    ]

Here we have 8 different themes. So in the dropdown also we need to have 8 options.

Let’s change that.


    options: [{
                value: 0,
                label: "Theme 1"
        },
        {
                value: 1,
                label: "Theme 2"
        },
        {
                value: 2,
                label: "Theme 2"
        },
        {
                value: 3,
                label: "Theme 2"
        },
        {
                value: 4,
                label: "Theme 2"
        },
        {
                value: 5,
                label: "Theme 2"
        },
        {
                value: 6,
                label: "Theme 2"
        },
        {
                value: 7,
                label: "Theme 2"
        }]

Here instead of Theme 1, 2 3.. we can use the bootstrap theme name directly.

i’m going to make this little dynamic here. instead of listing all theme in the options. I’m going to write a function which creates the options array automatically.

For this i’m going to declare this listThemes as a global variable. move this to top of the code.


    var listThemes = [
      'table-dark',
      'table-striped',
      'table-striped table-dark',
      'table-bordered',
      'table-bordered table-dark',
      'table-hover',
      'table-hover table-dark',
      'table-sm'
    ]

in the dropdown component definition, instead of this array, i’m going to write a function. 

In this function i have used an array function map which returns the value and label.


    options: function(){
      return listThemes.map(function(theme){
        return {
          value: index,
          label: theme
        };
      })
    }

I’ll show you how the output will come. let’s add console.log statement to check the value in the console.


    options: function(){
    
      console.log('themes dropdown', listThemes.map(function(theme){
        return {
          value: index,
          label: theme
        };
      }));
    
      return listThemes.map(function(theme){
        return {
          value: index,
          label: theme
        };
      })
    }

Save this file and refresh the page. And in the console you will see the options. So here we have value as well as label.

Even in future if we want to include more theme option, then we just need to modify the ‘listThemes’ array with the specific class name. And the dropdown will automatically show that value.

This function method to create the options is more powerful. If you want to populate these options by calling an external api you can do that. This opens lot of ideas in creating and customizing the extension.

Now in the table element class we just need to add the class name based on the theme index.


    $element.html(
        '<table class="table table-striped">' +
        '   <thead>' +
        header +
        '   </thead>' +
        '   <tbody>' +
        rows +
        '   </tbody>' +
        '</table>'
    );

Here in the class just concatenate the selected theme class. add two single quotes to break the line. and concatenate `listThemes[themeIndex]`


    $element.html(
        '<table class="table '+listThemes[themeIndex]+'">' +
        '   <thead>' +
        header +
        '   </thead>' +
        '   <tbody>' +
        rows +
        '   </tbody>' +
        '</table>'
    );

That’s it. Based on the selection in the property panel. Now the table style will be changed.

Let’s test that. If you refresh the page and go to the properties panel and select a theme. Your table will be styled accordingly.

Next we are going to create two more properties to control the alignment of the data and another is to hide and show the column based on a condition.

If you look at this at a high level it looks we need just two properties to achieve it. But we have more than one column in the table for dimension and measure. we need two properties  for each dimension and measure to control their  alignment and visibility.

If we add this property under setting then we may need to add this multiple times based on the number of dimension and measures.

So we cannot add this under settings. Instead we can add this in Dimension. Let’s add that.

The method is same,


    dimensions: {
        uses: "dimensions",
        min: 1,
        max: 2,
        items: {
          visibility: {
            type: "string",
            label: "Conditional Show",
            ref: "qDef.custom.conditionalShow"
          }
        }
    },

we need to add items property and in that add the item for controlling the visibility. So i have added the label conditional show.  For reference you cannot give any name here. because it is not like adding custom property under settings. This property has to repeat based for each dimension so we need to add provide the reference from ‘qDef’. So i gave ‘qDef.custom.conditionalShow’.

Let’s see the output. One thing to notice here is if you change anything on the dimension property you need to delete the dimension and add it back to make it work properly.

So let’s do that. 

Now if you check the dimension we have the option to specify the condition here. If i add one more dimension then…

This property will be available for that dimension too. So it is automatically taken care. If we add any additional property in the dimension then it gets added to all dimensions. It is same for measures too.

Now let’s see how to access this property. So go to the console and check the information returned by layout property.

In the console under qHypercube and qDimensionInfo, you have the property custom.conditionalShow.

We can change the value here it will reflect in the qDimensionInfo.

But the value is a plain string. there is no option to add any expression. to enable expression we need to add one more property in the custom property definition.


Let’s do that. the property name is expression and the value should be ‘always’ or ‘optional’.


    dimensions: {
        uses: "dimensions",
        min: 1,
        max: 2,
        items: {
          visibility: {
            type: "string",
            label: "Conditional Show",
            ref: "qDef.custom.conditionalShow",
            expression: "always"
          }
        }
    },

‘always’ means, whatever value you are giving here will be considered as expression. so if you want to provide a plain string you need to enclose it with single quote. 

if you use optional then you need to use equal sign to indicate that it is an expression.

Similarly let’s add an option to specify the text alignment.


    textAlignment: {
        type: "string",
        component: "buttongroup",
        label: "Text alignment",
        ref: "qDef.custom.textAlignment",
        options: [{
                value: "text-left",
                label: "left"
        }, {
                value: "text-center",
                label: "center"
        }, {
                value: "text-right",
                label: "right"
        }],
        defaultValue: "text-left"
    }

This is the code to add button group. Here i have mentioned the type as string, component as ‘buttongroup’ and label as Text alignment. Here also reference should start with qDef. similar to the ‘dropdown’ component here also we need to add options. Each option will be showed as button. In bootstrap we have a class name to align the text. I have given those values as  

Here the default value is left. Let’s text the output.

Let me re add the extension and delete the dimension and re-add it. Let’s check the console log. In qDimensionInfo we have these two properties one for conditional show and one for text alignment.

We have created all the custom property. Now as the last step we just need to use these property in the script.


    layout.qHyperCube.qDimensionInfo.forEach(function (dim) {
        if (dim.custom.conditionalShow != 0) {
            header += '<th>' + dim.qFallbackTitle + '</th>';
        }
    })

For hide and show we can simply add an if condition in the qDimensionInfo for loop and check for conditionalShow!=0.

here the property reference is custom.conditionalShow as mentioned in the property definition.

This will ignore the columns for which conditional show expression is false. But this will be applied only to the header. we need to repeat this for data as well.


    layout.qHyperCube.qDataPages[0].qMatrix.forEach(function (item, iteration) {
        var columns = '';
        item.forEach(function (col, i) {
            if (i < layout.qHyperCube.qDimensionInfo.length) {
                if (dim.custom.conditionalShow != 0) {
                    columns += '<td dim-id="' + i + '" data-id="' + col.qElemNumber + '">' + col.qText + '</td>';
                }
            } else {
                columns += '<td>' + col.qText + '</td>';
            }
        })
        rows += '<tr>' +
            columns +
            '</tr>';
    });

For this we need add the same if condition in the matrix for loop. if you remember we have added a condition here already to check whether the column is a dimension or measure.

if i is less than dimensioninfo length then it is a dimension so we need to add an if condition here to check for conditionalShow not equal to zero.

But we cannot use just dim dot custom dot conditionalShow. Because we are not looping over the dimension info here. This ’i’ variable indicates the column number so instead of dim we can simply use “layout.qHyperCube.qDimensionInfo[i]”.



    layout.qHyperCube.qDataPages[0].qMatrix.forEach(function (item, iteration) {
        var columns = '';
        item.forEach(function (col, i) {
            if (i < layout.qHyperCube.qDimensionInfo.length) {
                if (layout.qHyperCube.qDimensionInfo[i].custom.conditionalShow != 0) {
                    columns += '<td dim-id="' + i + '" data-id="' + col.qElemNumber + '">' + col.qText + '</td>';
                }
            } else {
                columns += '<td>' + col.qText + '</td>';
            }
        })
        rows += '<tr>' +
            columns +
            '</tr>';
    });

Similarly for text alignment we can just add  the class based on the custom property. which is again `layout.qHyperCube.qDimensionInfo[i].custom.textAlignment`

Jus add a class name variable and store the `textAligment` property. And add that as a class in the td element.


    layout.qHyperCube.qDataPages[0].qMatrix.forEach(function (item, iteration) {
        var columns = '';
        item.forEach(function (col, i) {
            if (i < layout.qHyperCube.qDimensionInfo.length) {
                var classsName =layout.qHyperCube.qDimensionInfo[i].custom.textAlignment;
                if (layout.qHyperCube.qDimensionInfo[i].custom.conditionalShow != 0) {
                    columns += '<td class="'+classsName+'" dim-id="' + i + '" data-id="' + col.qElemNumber + '">' + col.qText + '</td>';
                }
            } else {
                columns += '<td>' + col.qText + '</td>';
            }
        })
        rows += '<tr>' +
            columns +
            '</tr>';
    });

Let’s test the output.Refresh the page.

Now if i add any condition here say `1==0` which is always false. so this column is not visible here.

if i say `1=1` or if i don’t mention any condition then the column will be visible in the UI. Also if i change the text alignment it is getting reflected here.

I’m going to stop here. But we didn’t achieve this functionality for measures. Please try that yourself so that it will be a small exercise for you to recollect what we did here.

I will provide that code in the github for your reference. So you can compare your method with mine.

Also it is not the only way you can achieve the said functionality. This is just an idea on how to add properties at dimension level as well as at extension level. you can use this to achieve you own requirement.

Hope this video is helpful. Please subscribe to this channel if you want more videos like this and provide your feedback in the comment section.

Thanks for watching will see you in the next video.

