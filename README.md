Fluid feathers
==============

Skatch-up of fluent interfaces for declarative description of GUI in FeathersUI also Starling framework.
Inspired by Sibirjak DataProvider Controls Examples [https://github.com/kakenbok/ActionScript-DataProvider-Controls]


Examples
========

## Form

![HelloWorld Form](http://i.imgur.com/BxTQx.png)

```actionscript
var b : UIBuilder = getUIBuilder();

var container : DisplayObject = b.vGroup()
	.gap(16)
	.contain(
		b.label()
			.text("Hello World!")
			.build(),
		b.hGroup()
			.contain(
				b.label()
					.text("Long Blah-Blah-Blah\nBlah-Blah-Blah\nBlah-Blah-Blah\nBlah-Blah-Blah!")
					.build()
			).build(),
		b.hGroup()
			.gap(4)
			.contain(
				b.button()
					.label("Help")
					.onTriggered(onButtonTriggered)
					.build(),
				b.button()
					.label("Ok")
					.onTriggered(onButtonTriggered)
					.build(),
				b.button()
					.label("Cancel")
					.onTriggered(onButtonTriggered)
					.build()
			).build()
	)
	.x(20).y(20)
	.width(stage.stageWidth)
	.height(stage.stageHeight)
	.buildAndAddTo(this);
```

## Button and Label

```actionscript

//Before -----------------------------------------------------

_button = new Button();
_button.label = "Click Me";
_button.addEventListener(Event.TRIGGERED, button_triggeredHandler);
_button.x = 200;
_button.y = 200;
addChild(_button);

var label:Label = new Label();
label.text = "Hello World!";
label.x = 50;
label.y = 200;
addChild(label);

//After -----------------------------------------------------

var b : UIBuilder = getUIBuilder();

_button = b.button()
			.label("Click Me")
			.onTriggered(button_triggeredHandler)
			.x(200)
			.y(200)
			.buildAndAddTo(this) as Button;

b.label()
	.text("Hello World!")
	.x(50)
	.y(200)
	.buildAndAddTo(this);

```

## List

```actionscript

//Before -----------------------------------------------------

var buttonA:Button = new Button();
buttonA.label = "Click Me A";
buttonA.addEventListener(Event.TRIGGERED, button_triggeredHandler);

var buttonB:Button = new Button();
buttonB.label = "Click Me B";
buttonB.addEventListener(Event.TRIGGERED, button_triggeredHandler);

var label:Label = new Label();
label.text = "Hello World!";

var listPicker:PickerList = new PickerList();
listPicker.dataProvider = new ListCollection([
	{label:"item A"},
	{label:"item B"},
	{label:"item C"}
]);

_list = new List();
_list.isSelectable = false;
_list.dataProvider = new ListCollection(
	[
		{ label: "button A", accessory: buttonA },
		{ label: "button B", accessory: buttonB },
		{ label: "label", accessory: label },
		{ label: "listPicker", accessory: listPicker }
	]);			
addChild(_list);

_list.x = 0;
_list.y = 0;
_list.width = stage.stageWidth;
_list.height = stage.stageHeight;

//After -----------------------------------------------------

var b : UIBuilder = getUIBuilder();
_list = b.list()
			.dataProvider(new ListCollection([
				{ 
					label: "button A", 
					accessory: b.button()
									.label("Click Me A")
									.onTriggered(button_triggeredHandler)
									.build()
				},
				{ 
					label: "button B", 
					accessory: b.button()
									.label("Click Me B")
									.onTriggered(button_triggeredHandler)
									.build()
				},
				{ 
					label: "label", 
					accessory: b.label()
									.text("Hello World!")
									.build()
				},
				{ 
					label: "listPicker", 
					accessory: b.pickerList()
									.dataProvider(new ListCollection([
										{label:"item A"},
										{label:"item B"},
										{label:"item C"}
									]))
									.build()
				}
			]))
			.selectable(false)
			.x(0).y(0)
			.width(stage.stageWidth)
			.height(stage.stageHeight)
			.buildAndAddTo(this) as List;

```