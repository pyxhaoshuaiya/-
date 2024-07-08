# My homework
这是一个课程作业。该教程的完整文件为experiment_2.html。
# 实验制作教程：情绪stroop（experiment_2)
*本教程将引导你通过编写一个基于Stroop效应的简单反应时实验。实验任务是识别字体颜色，并根据颜色按下相应的键。这个实验不仅涵盖了jsPsych库的基本使用，还介绍了如何结合多种插件创建试次、插入图片、使用时间线变量以及数据记录和反馈。*

## 第一部分：初始化实验
我们首先创建一个HTML文件，并引入`jsPsych`、`html-keyboard-response`插件和`jspsych.css`等文件。现在，你的HTML文件应该是这样的：
```js
<!DOCTYPE  html>
<html>
	<head>
		<title>My experiment</title>
		<script  src="https://unpkg.com/jspsych@7.3.4"></script>
		<script  src="https://unpkg.com/@jspsych/plugin-html-keyboard-response@1.1.3"></script>
		<link  href="https://unpkg.com/jspsych@7.3.4/css/jspsych.css"  rel="stylesheet"  type="text/css"  />
	</head>
	<body></body>
	<script>
	</script>
</html>
```
## 第2部分：呈现欢迎内容
首先，我们必须初始化 jsPsych。在这里可以引入`initJsPsych()`函数。
```js
var  jsPsych = initJsPsych();
```
接着，我们需要引入一条时间线。
```js
var  timeline = [];
```
然后我们定义一个欢迎试次作为实验的开头，并引入按键反应插件：`jsPsychHtmlKeyboardResponse`。
```js
var  welcome = {
	type:  jsPsychHtmlKeyboardResponse,
	stimulus:  "Welcome to the experiment. Press any key to begin."
};
```
把这个试次推送到时间线。
```js
timeline.push(welcome);
```
通过调用`jspsych.run()`函数运行实验。
```js
jspsych.run(timeline);
```

## 第3部分：实验指导

第3部分与第2部分的方法类似，为了让被试更好地理解实验，我们需要制作实验指导语，使用HTML格式的字符串呈现多行文本，并设置间隔时间，在本实验中时间间隔被设置为2000ms。
```js
/* define instructions trial */
var  instructions = {
	type:  jsPsychHtmlKeyboardResponse,
	stimulus:  `
		<p style="font-size:30px;">Now we're going to conduct an experiment on color recognition.</p>
		<p style="font-size:30px;">The first thing that will appear on the screen is a “+” fixation.</p>
		<p style="font-size:30px;">After that a picture with a certain mood will appear.</p>
		<p style="font-size:30px;">After the picture disappears, you will see a word.</p>
		<p style="font-size:30px;">Press the “R” key if the font color is red.</p>
		<p style="font-size:30px;">Press the “G” key if the font color is green.</p>
		<p style="font-size:30px;">Press the “B” key if the font color is blue.</p>
		<div style='width: 700px;'>
		</div>
		<p style="font-size:30px;">Press any key to start the experiment.</p>
	`,
	post_trial_gap:2000
};
timeline.push(instructions);
```
## 第4部分：定义试次

在这个部分，我们需要创建多个试次，我们的实验中需要用到图片，因此首先在`<head>`部分引入`image-keyboard-response`插件。
```js
<script  src="https://unpkg.com/@jspsych/plugin-image-keyboard-response@1.1.3"></script>
```
接着我们需要对实验试次进行定义，使用`jsPsychHtmlKeyboardResponse`插件来呈现单词并记录反应。以红色的一致试次为例，我们需要在屏幕上显示一个红色的“red”，且只有按下"r"、"g"、"b"键被认为是有效的。代码如下：
```js
/*define trials*/
var  red1_trail={
	type:  jsPsychHtmlKeyboardResponse,
	stimulus:`<p style="font-size:50px;color:red;">red</p>`,
	choices:['r','g','b']
}
// 略去其他试次的定义...
```
完成该部分的编写后完整代码如下：
```js
<!DOCTYPE  html>
<html>
	<head>
		<title>My experiment</title>
		<script  src="https://unpkg.com/jspsych@7.3.4"></script>
		<script  src="https://unpkg.com/@jspsych/plugin-html-keyboard-response@1.1.3"></script>
		<link  href="https://unpkg.com/jspsych@7.3.4/css/jspsych.css"  rel="stylesheet"  type="text/css"  />
	</head>
<body>
</body>
<script>
	/* initialize jsPsych */
	var  jsPsych = initJsPsych();
	  
	/* create timeline */
	var  timeline = [];
	  
	/* define welcome message trial */
	var  welcome = {
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:  "Welcome to the experiment. Press any key to begin."
	};
	timeline.push(welcome);
	  
	/* define instructions trial */
	var  instructions = {
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:  `
			<p style="font-size:30px;">Now we're going to conduct an experiment on color recognition.</p>
			<p style="font-size:30px;">The first thing that will appear on the screen is a “+” fixation.</p>
			<p style="font-size:30px;">After that a picture with a certain mood will appear.</p>
			<p style="font-size:30px;">After the picture disappears, you will see a word.</p>
			<p style="font-size:30px;">Press the “R” key if the font color is red.</p>
			<p style="font-size:30px;">Press the “G” key if the font color is green.</p>
			<p style="font-size:30px;">Press the “B” key if the font color is blue.</p>
			<div style='width: 700px;'>
			</div>
			<p style="font-size:30px;">Press any key to start the experiment.</p>
		`,
		post_trial_gap:2000
	};
	timeline.push(instructions);
	
	/*define trials*/
	var  red1_trail={
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:`<p style="font-size:50px;color:red;">red</p>`,
		choices:['r','g','b']
	}

	var  green1_trail={
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:`<p style="font-size:50px;color:green;">green</p>`,
		choices:['r','g','b']
	}
	  
	var  blue1_trail={
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:`<p style="font-size:50px;color:blue;">blue</p>`,
		choices:['r','g','b']
	}

	var  red2_trail={
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:`<p style="font-size:50px;color:green;">red</p>`,
		choices:['r','g','b']
	}

	var  green2_trail={
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:`<p style="font-size:50px;color:blue;">green</p>`,
		choices:['r','g','b']
	}
	  
	var  blue2_trail={
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:`<p style="font-size:50px;color:red;">blue</p>`,
		choices:['r','g','b']
	}

	var  red3_trail={
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:`<p style="font-size:50px;color:red;">mouse</p>`,
		choices:['r','g','b']
	}

	var  green3_trail={
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:`<p style="font-size:50px;color:green;">monkey</p>`,
		choices:['r','g','b']
	}

	var  blue3_trail={
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:`<p style="font-size:50px;color:blue;">magpie</p>`,
		choices:['r','g','b']
	}

	/* start the experiment */
		jsPsych.run(timeline);
</script>
</html>
```
## 第5部分：预加载多媒体

在实验中，无论何时使用多媒体元素（图片、音频或视频），最好在需要它们进行试验之前先进行预加载。通过预加载多媒体，我们请求参与者的浏览器提前下载媒体，这样当我们需要显示或播放它们时，就不会出现因为需要下载而造成的延迟。
我们将使用预加载插件来预加载这些图片。多媒体预加载部分详细介绍了预加载的各种选项以及您可以使用此插件的不同方式。在这里，我们将简单地给插件一个我们希望预加载的文件列表。
首先，我们需要将预加载插件添加到我们的`<head>`部分。
```js
<script  src="https://unpkg.com/@jspsych/plugin-preload@1.1.3"></script>
```
我们将这个试次放在实验的最开始，并把它推送到时间线上。注意，实验中所需要的图片需要提前保存在实验文件夹中，在本实验中，我们把图片保存在实验文件夹中的images文件夹中。
```js
var  preload = {
	type:  jsPsychPreload,
	images: ['images/a1.png', 'images/a2.png', 'images/a3.png', 'images/a4.png', 'images/b1.png', 'images/b2.png', 'images/b3.png', 'images/b4.png', 'images/c1.png', 'images/c2.png', 'images/c3.png', 'images/c4.png', ]
};
timeline.push(preload);
```
在此展示实验中所用到的图片供大家下载。
![a1](images/a1.png)
![a2](https://yesicon.app/noto/kissing-face-with-closed-eyes)
![a3](https://yesicon.app/noto/partying-face)
![a4](https://yesicon.app/noto/star-struck)
## 第6部分：时间线变量

在一个完整的实验中，我们将需要很多的试次。我们可以创建更多的对象来定义试次，并将它们全部添加到时间线上，但有一个更高效的方法：使用时间线变量。
首先，让我们创建一个数组，其中包含我们在测试阶段想要运行的所有不同试次。
```js
var  test_stimuli = [
	{ stimulus:  `<p style="font-size:50px;color:red;">red</p>`},
	{ stimulus:  `<p style="font-size:50px;color:green;">green</p>`},
	{ stimulus:  `<p style="font-size:50px;color:blue;">blue</p>`},
	{ stimulus:  `<p style="font-size:50px;color:green;">red</p>`},
	{ stimulus:  `<p style="font-size:50px;color:blue;">green</p>`},
	{ stimulus:  `<p style="font-size:50px;color:red;">blue</p>`},
	{ stimulus:  `<p style="font-size:50px;color:red;">mouse</p>`},
	{ stimulus:  `<p style="font-size:50px;color:green;">monkey</p>`},
	{ stimulus:  `<p style="font-size:50px;color:blue;">magpie</p>`},
];
```
除了展示不同颜色的单词之外，让我们还设置实验在试次之间展示一个注视点（+）。我们可以通过使用`html-keyboard-response`插件的参数，并将其设置为特殊值`"NO_KEYS"`，来定义一个试次来展示注视点一段固定的时间。这个特殊值意味着没有响应会被视为有效响应，试次将持续参数所指定的时间。
```js
var fixation = {
  type: jsPsychHtmlKeyboardResponse,
  stimulus: '<div style="font-size:60px;">+</div>',
  choices: "NO_KEYS",
  trial_duration: 1000,
};
```
在注视点呈现完毕之后，将随机呈现图片，我们同样需要为图片创建一个数组。
```js
var  img_sti = [
	{sti:'images/a1.png'},
	{sti:'images/a2.png'},
	{sti:'images/a3.png'},
	{sti:'images/a4.png'},
	{sti:'images/b1.png'},
	{sti:'images/b2.png'},
	{sti:'images/b3.png'},
	{sti:'images/b4.png'},
	{sti:'images/c1.png'},
	{sti:'images/c2.png'},
	{sti:'images/c3.png'},
	{sti:'images/c4.png'}
];
```
为了随机展示试次，我们将使用`image-keyboard-response`插件设置另一个试次，但我们将使用`jsPsych.timelineVariable()`函数来指示我们希望jsPsych从时间线变量中替换参数值。
```js
var test = {
  type: jsPsychImageKeyboardResponse,
  stimulus: jsPsych.timelineVariable('stimulus'),
  choices: ['r','g','b']
};

var  img = {
	type:jsPsychImageKeyboardResponse,
	stimulus:jsPsych.timelineVariable('sti'),
	choices:"NO_KEYS",
	trial_duration:  500
};
```
为了让jsPsych知道调用`jsPsych.timelineVariable()`的时候是要从`test_stimuli`数组中取值，我们还需要创建一条新的时间线，并为其添加`timeline_variables`属性。同时，为了在一个试次中随机呈现一张图片，在这里我们引入`sample`参数，有重复地从时间线中抽取一张图片。
```js
var  img_procedure = {
	timeline: [fixation, img],
	timeline_variables:  img_sti,
	sample:{
	type:  'with-replacement',
	size:  1
	}
};
```
接着再创建一条时间线，把注视点、抽取好的图片同单词连接起来，用`randomize_order`参数让单词随机呈现，并将整个数组的重复次数设置为5。
```js
var  test_procedure = {
	timeline:[img_procedure, test],
	timeline_variables:test_stimuli,
	randomize_order:true,
	repetitions:5
};
```
## 第7部分：启动实验
最后，使用`jsPsych.run(timeline)`启动实验：
```js
/* start the experiment */  
jsPsych.run(timeline);
```
到这里我们的程序就基本完成了，下面是完整代码。
```js
<!DOCTYPE  html>
<html>
<head>
	<title>My experiment</title>
	<script  src="https://unpkg.com/jspsych@7.3.4"></script>
	<script  src="https://unpkg.com/@jspsych/plugin-html-keyboard-response@1.1.3"></script>
	<script  src="https://unpkg.com/@jspsych/plugin-image-keyboard-response@1.1.3"></script>
	<script  src="https://unpkg.com/@jspsych/plugin-preload@1.1.3"></script>
	<link  href="https://unpkg.com/jspsych@7.3.4/css/jspsych.css"  rel="stylesheet"  type="text/css"  />
</head>
<body>
</body>
<script>

	/* initialize jsPsych */
	var  jsPsych = initJsPsych();

	/* create timeline */

	var  timeline = [];

	var  preload = {
		type:  jsPsychPreload,
		images: ['images/a1.png', 'images/a2.png', 'images/a3.png', 'images/a4.png', 'images/b1.png', 'images/b2.png', 'images/b3.png', 'images/b4.png', 'images/c1.png', 'images/c2.png', 'images/c3.png', 'images/c4.png', ]
	};
	timeline.push(preload);

	/* define welcome message trial */
	var  welcome = {
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:  `<p style="font-size:30px;">Welcome to the experiment. Press any key to begin.</p>`
	};
	timeline.push(welcome);

	/* define instructions trial */
	var  instructions = {
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:  `
			<p style="font-size:30px;">Now we're going to conduct an experiment on color recognition.</p>
			<p style="font-size:30px;">The first thing that will appear on the screen is a “+” fixation.</p>
			<p style="font-size:30px;">After that a picture with a certain mood will appear.</p>
			<p style="font-size:30px;">After the picture disappears, you will see a word.</p>
			<p style="font-size:30px;">Press the “R” key if the font color is red.</p>
			<p style="font-size:30px;">Press the “G” key if the font color is green.</p>
			<p style="font-size:30px;">Press the “B” key if the font color is blue.</p>
			<div style='width: 700px;'>
			</div>
			<p style="font-size:30px;">Press any key to start the experiment.</p>
		`,
		post_trial_gap:2000
	};
	timeline.push(instructions);

	/*define timeline variable*/
		var  test_stimuli = [
		{ stimulus:  `<p style="font-size:50px;color:red;">red</p>`,correct_response:'r'},
		{ stimulus:  `<p style="font-size:50px;color:green;">green</p>`,correct_response:'g'},
		{ stimulus:  `<p style="font-size:50px;color:blue;">blue</p>`,correct_response:'b'},
		{ stimulus:  `<p style="font-size:50px;color:green;">red</p>`,correct_response:'g'},
		{ stimulus:  `<p style="font-size:50px;color:blue;">green</p>`,correct_response:'b'},
		{ stimulus:  `<p style="font-size:50px;color:red;">blue</p>`,correct_response:'r'},
		{ stimulus:  `<p style="font-size:50px;color:red;">mouse</p>`,correct_response:'r'},
		{ stimulus:  `<p style="font-size:50px;color:green;">monkey</p>`,correct_response:'g'},
		{ stimulus:  `<p style="font-size:50px;color:blue;">magpie</p>`,correct_response:'b'},
	];

	var  img_sti = [
		{sti:'images/a1.png'},
		{sti:'images/a2.png'},
		{sti:'images/a3.png'},
		{sti:'images/a4.png'},
		{sti:'images/b1.png'},
		{sti:'images/b2.png'},
		{sti:'images/b3.png'},
		{sti:'images/b4.png'},
		{sti:'images/c1.png'},
		{sti:'images/c2.png'},
		{sti:'images/c3.png'},
		{sti:'images/c4.png'},
	];
	
	var  fixation = {
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:  '<div style="font-size:60px;">+</div>',
		choices:  "NO_KEYS",
		trial_duration:  function(){
			return  jsPsych.randomization.sampleWithoutReplacement([250, 500, 750, 1000, 1250, 1500, 1750, 2000], 1)[0];
		},
		data: {
			task:  'fixation'
		}
	}

	var  test = {
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:  jsPsych.timelineVariable('stimulus'),
		choices: ['r','g','b'],
		data:{
			task:'response',
			correct_response:  jsPsych.timelineVariable('correct_response')
		},
		on_finish:  function(data){
			data.correct = jsPsych.pluginAPI.compareKeys(data.response, data.correct_response);
		}
	};

	var  img = {
		type:jsPsychImageKeyboardResponse,
		stimulus:jsPsych.timelineVariable('sti'),
		choices:"NO_KEYS",
		trial_duration:  500
		};  

	var  img_procedure = {
		timeline: [fixation, img],
		timeline_variables:  img_sti,
		sample:{
			type:  'with-replacement',
			size:  1
		}
	};

	var  test_procedure = {
		timeline:[img_procedure, test],
		timeline_variables:test_stimuli,
		randomize_order:true,
		repetitions:5
	};
	timeline.push(test_procedure);
	var  endpage={
		type:  jsPsychHtmlKeyboardResponse,
		stimulus:`<p style="font-size:50px;color:red;">The experiment is over. Thank you for your participation.</p>`
		};
		timeline.push(endpage);

	/* start the experiment */
	jsPsych.run(timeline);
</script>
</html>
```
