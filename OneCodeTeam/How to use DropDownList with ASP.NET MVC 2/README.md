# How to use DropDownList with ASP.NET MVC
## Requires
- Visual Studio 2013
## License
- Apache License, Version 2.0
## Technologies
- ASP.NET
- ASP.NET MVC 4
## Topics
- DropDownList
## Updated
- 01/02/2014
## Description

<hr>
<div><a href="http://blogs.msdn.com/b/onecode" style="margin-top:3px"><img alt="" src="http://bit.ly/onecodesampletopbanner">
</a></div>
<h1>Cascading DropDown List with ASP.NET MVC 4</h1>
<h2>Introduction</h2>
<p class="MsoNormal"><a href="http://www.asp.net/mvc/mvc4">ASP.NET MVC 4</a> is a framework for building scalable, standards-based web applications using well-established design patterns and the power of ASP.NET and the .NET Framework. This article and the
 attached code samples demonstrate demonstrates how to use cascading dropdown list with ASP.NET MVC 4.<span style="">&nbsp;
</span>You can find the answers for all the following questions in the code sample:</p>
<p class="MsoListParagraphCxSpFirst" style="text-indent:-.25in"><span style="font-family:Symbol"><span style="">&bull;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span>How to create a simple dropdown list</p>
<p class="MsoListParagraphCxSpMiddle" style="text-indent:-.25in"><span style="font-family:Symbol"><span style="">&bull;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span>How to post data to server when dropdown list selected item changed</p>
<p class="MsoListParagraphCxSpMiddle" style="text-indent:-.25in"><span style="font-family:Symbol"><span style="">&bull;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span>How to implement cascaded DropDownList</p>
<p class="MsoListParagraphCxSpMiddle" style="text-indent:-.25in"><span style="font-family:Symbol"><span style="">&bull;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span>How to update the local section accroding to the item selected</p>
<p class="MsoListParagraphCxSpLast" style="text-indent:-.25in"><span style="font-family:Symbol"><span style="">&bull;<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span>How to dynamically generate options for dropdown list</p>
<h2>Running the Sample</h2>
<p class="MsoNormal">You must run this code sample on Visual Studio 2012 or newer versions.</p>
<p class="MsoNormal">After you successfully build the sample project in Visual Studio 2012, you will get the &quot;CascadingDropDown Demonstration in ASP.NET MVC 4&quot; web-page.</p>
<p class="MsoNormal"><span style=""><img src="106353-image.png" alt="" width="559" height="268" align="middle">
</span></p>
<p class="MsoNormal">Select any <b style="">Make</b> from the available options. This will make a server call to get the models</p>
<p class="MsoNormal"><span style=""><img src="106354-image.png" alt="" width="557" height="308" align="middle">
</span></p>
<p class="MsoNormal">Select <b style="">Model </b>from the available options. This will make a server call to get the colors</p>
<p class="MsoNormal"><span style=""><img src="106355-image.png" alt="" width="549" height="271" align="middle">
</span></p>
<h2>Using the Code</h2>
<h3>How to use controller?</h3>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp">


namespace VBDropdownListMVC4.Controllers


{


&nbsp;&nbsp;&nbsp; /// &lt;summary&gt;


&nbsp;&nbsp;&nbsp; /// Controller class for sample


&nbsp;&nbsp;&nbsp; /// &lt;/summary&gt;


&nbsp;&nbsp;&nbsp; public class CascadingDropDownSampleController : Controller


&nbsp;&nbsp;&nbsp; {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #region
&quot;Public Actions&quot;






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;summary&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// Default Action for the web-page handling HTTP GET requests


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;/summary&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;returns&gt;&lt;/returns&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [HttpGet]


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; public ActionResult Index()


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; IDictionary&lt;string, string&gt; makes = GetSampleMakes();


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; CascadingDropDownSampleModel viewModel = new CascadingDropDownSampleModel()


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Makes = makes


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; };






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return View(viewModel);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;summary&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// AJAX Action to send sample Models in JSON format based on
the selected make


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;/summary&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;param
name=&quot;selectedMake&quot;&gt;&lt;/param&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;returns&gt;&lt;/returns&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; public ActionResult GetSampleModels(string selectedMake)


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; IDictionary&lt;string, string&gt; models = GetSampleModelsFromSelectedMake(selectedMake);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return Json(models);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;summary&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// AJAX Action to send sample colors in JSON format based on
the selected model


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;/summary&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;param name=&quot;selectedModel&quot;&gt;&lt;/param&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;returns&gt;&lt;/returns&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; public ActionResult GetSampleColors(string selectedModel)


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; IDictionary&lt;string, string&gt; colors =
GetSampleColorsFromSelectedModel(selectedModel);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return Json(colors);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #endregion






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #region
&quot;Private Methods&quot;






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;summary&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// Method to generate sample makes


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;/summary&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;returns&gt;&lt;/returns&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; private IDictionary&lt;string, string&gt; GetSampleMakes()


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; IDictionary&lt;string, string&gt; makes = new Dictionary&lt;string, string&gt;();






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; makes.Add(&quot;1&quot;, &quot;Acura&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; makes.Add(&quot;2&quot;, &quot;Audi&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; makes.Add(&quot;3&quot;, &quot;BMW&quot;);






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return makes;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;summary&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// Method to generate sample models based on selected make


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;/summary&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;param
name=&quot;selectedMake&quot;&gt;&lt;/param&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;returns&gt;&lt;/returns&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; private IDictionary&lt;string, string&gt; GetSampleModelsFromSelectedMake(string selectedMake)


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; IDictionary&lt;string, string&gt; models = new Dictionary&lt;string, string&gt;();






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; switch (selectedMake)


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; case &quot;1&quot;:


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; models.Add(&quot;1&quot;, &quot;Integra&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;models.Add(&quot;2&quot;, &quot;RL&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; models.Add(&quot;3&quot;, &quot;TL&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; break;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; case &quot;2&quot;:


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; models.Add(&quot;4&quot;, &quot;A4&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; models.Add(&quot;5&quot;, &quot;S4&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; models.Add(&quot;6&quot;, &quot;A6&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;break;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; case &quot;3&quot;:


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; models.Add(&quot;7&quot;, &quot;3 series&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; models.Add(&quot;8&quot;, &quot;5 series&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; models.Add(&quot;9&quot;, &quot;7 series&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; break;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; default:


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;throw new NotImplementedException();






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return models;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;summary&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// Method to generate sample colors based on selected model


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;/summary&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;param
name=&quot;selectedModel&quot;&gt;&lt;/param&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /// &lt;returns&gt;&lt;/returns&gt;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; private IDictionary&lt;string, string&gt; GetSampleColorsFromSelectedModel(string selectedModel)


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; IDictionary&lt;string, string&gt; colors = new Dictionary&lt;string, string&gt;();






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; switch (selectedModel)


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; case &quot;1&quot;:


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;1&quot;, &quot;Green&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;2&quot;, &quot;Sea Green&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;3&quot;, &quot;Pale Green&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; break;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; case &quot;2&quot;:


&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;colors.Add(&quot;4&quot;, &quot;Red&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;5&quot;, &quot;Bright Red&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; break;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; case &quot;3&quot;:


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;6&quot;, &quot;Teal&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;7&quot;, &quot;Dark Teal&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;break;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; case &quot;4&quot;:


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;8&quot;, &quot;Azure&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;9&quot;, &quot;Light Azure&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;10&quot;, &quot;Dark Azure&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; break;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; case &quot;5&quot;:


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;colors.Add(&quot;11&quot;, &quot;Silver&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;12&quot;, &quot;Metallic&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; break;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; case &quot;6&quot;:


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;13&quot;, &quot;Cyan&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; break;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; case &quot;7&quot;:


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;14&quot;, &quot;Blue&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;15&quot;, &quot;Sky Blue&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;16&quot;, &quot;Racing Blue&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; break;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; case &quot;8&quot;:


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;17&quot;, &quot;Yellow&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;18&quot;, &quot;Red&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; break;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; case &quot;9&quot;:


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; colors.Add(&quot;17&quot;, &quot;Brown&quot;);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; break;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; default:


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; throw new NotImplementedException();






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; return colors;


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; #endregion






&nbsp;&nbsp;&nbsp; }


}</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">namespace</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:black">VBDropdownListMVC4<span style="background:white">.Controllers
</span></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">{
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;summary&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white"> Controller class for sample</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;/summary&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">public</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">class</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">CascadingDropDownSampleController</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> :
</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">Controller</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span>{ </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>#region</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> &quot;Public Actions&quot;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;summary&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white"> Default Action for the web-page handling HTTP GET requests</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;/summary&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;returns&gt;&lt;/returns&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>[</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">HttpGet</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">]
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">public</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">ActionResult</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> Index()
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>{ </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">IDictionary</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&lt;</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&gt; makes = GetSampleMakes();
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">CascadingDropDownSampleModel</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> viewModel =
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">new</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">CascadingDropDownSampleModel</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">()
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>{ </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>Makes = makes </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>}; </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">return</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> View(viewModel);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>} </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;summary&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white"> AJAX Action to send sample Models in JSON format based on the selected
 make</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;/summary&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;param name=&quot;selectedMake&quot;&gt;&lt;/param&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;returns&gt;&lt;/returns&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">public</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">ActionResult</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> GetSampleModels(</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
 selectedMake) </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>{ </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">IDictionary</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&lt;</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&gt; models = GetSampleModelsFromSelectedMake(selectedMake);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">return</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> Json(models);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>} </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;summary&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white"> AJAX Action to send sample colors in JSON format based on the selected
 model</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;/summary&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;param name=&quot;selectedModel&quot;&gt;&lt;/param&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;returns&gt;&lt;/returns&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">public</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">ActionResult</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> GetSampleColors(</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
 selectedModel) </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>{ </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">IDictionary</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&lt;</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&gt; colors = GetSampleColorsFromSelectedModel(selectedModel);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">return</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> Json(colors);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>} </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>#endregion</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>#region</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> &quot;Private Methods&quot;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;summary&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white"> Method to generate sample makes</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;/summary&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;returns&gt;&lt;/returns&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">private</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">IDictionary</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&lt;</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&gt; GetSampleMakes()
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;</span><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>{ </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">IDictionary</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&lt;</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&gt; makes =
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">new</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">Dictionary</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&lt;</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&gt;();
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>makes.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;1&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Acura&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>makes.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;2&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Audi&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>makes.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;3&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;BMW&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">return</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> makes;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>} </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;summary&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white"> Method to generate sample models based on selected make</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;/summary&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;param name=&quot;selectedMake&quot;&gt;&lt;/param&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;returns&gt;&lt;/returns&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">private</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">IDictionary</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&lt;</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&gt; GetSampleModelsFromSelectedMake(</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
 selectedMake) </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>{ </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">IDictionary</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&lt;</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&gt; models =
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">new</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">Dictionary</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&lt;</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&gt;();
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">switch</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> (selectedMake)
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>{ </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">case</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;1&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">:
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>models.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;1&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Integra&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span><span style="">&nbsp;</span>models.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;2&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;RL&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>models.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;3&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;TL&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">break</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">case</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;2&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">:
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>models.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;4&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;A4&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>models.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;5&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;S4&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>models.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;6&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;A6&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">break</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">case</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;3&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">:
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>models.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;7&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;3 series&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>models.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;8&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;5 series&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>models.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;9&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;7 series&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">break</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">default</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">:
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">throw</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">new</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">NotImplementedException</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">();
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>} </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">return</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> models;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>} </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;summary&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white"> Method to generate sample colors based on selected model</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;/summary&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;param name=&quot;selectedModel&quot;&gt;&lt;/param&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">///</span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:gray; background:white">&lt;returns&gt;&lt;/returns&gt;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">private</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">IDictionary</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&lt;</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&gt; GetSampleColorsFromSelectedModel(</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
 selectedModel) </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>{ </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">IDictionary</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&lt;</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&gt; colors =
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">new</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">Dictionary</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&lt;</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">string</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">&gt;();
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">switch</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> (selectedModel)
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>{ </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">case</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;1&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">:
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;1&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Green&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;2&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Sea Green&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;3&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Pale Green&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">break</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">case</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;2&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">:
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;4&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Red&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;5&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Bright Red&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">break</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">case</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;3&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">:
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;6&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Teal&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;7&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Dark Teal&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span><span style="">&nbsp;&nbsp;&nbsp;</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">break</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">case</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;4&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">:
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;8&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Azure&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;9&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Light Azure&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;10&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Dark Azure&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">break</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">case</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;5&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">:
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span><span style="">&nbsp;&nbsp;&nbsp;</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;11&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Silver&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;12&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Metallic&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">break</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">case</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;6&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">:
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;13&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Cyan&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">break</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">case</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;7&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">:
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;14&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Blue&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;15&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Sky Blue&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;16&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Racing Blue&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">break</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">case</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;8&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">:
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;17&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Yellow&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;18&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Red&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">break</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">case</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;9&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">:
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>colors.Add(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;17&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;Brown&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">break</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">default</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">:
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">throw</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">new</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span><span style="font-size:9.5pt; font-family:Consolas; color:#2B91AF; background:white">NotImplementedException</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">();
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>} </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">return</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> colors;
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>} </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>#endregion</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span>} </span></p>
<h3>How to use Javascript?</h3>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>JavaScript</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">js</span>

<pre id="codePreview" class="js">


$(function () {


&nbsp;&nbsp;&nbsp; var cascadingDropDownSample = new CascadingDropDownSample();






&nbsp;&nbsp;&nbsp; //binding
change event of the &quot;make&quot; select HTML control


&nbsp;&nbsp;&nbsp; $('#make').on('change', function () {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; var selectedMake = $(this).val();






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; //if
selected other than default option, make a AJAX call to server


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; if (selectedMake !== &quot;-1&quot;) {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $.post('/CascadingDropDownSample/GetSampleModels',


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; { selectedMake: selectedMake },


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; function (data) {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
cascadingDropDownSample.resetCascadingDropDowns();


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
cascadingDropDownSample.getSampleModelsSuccess(data);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; });


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; else {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; //reset
the cascading dropdown


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
cascadingDropDownSample.resetCascadingDropDowns();


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }


&nbsp;&nbsp;&nbsp; });






&nbsp;&nbsp;&nbsp; //binding
change event of the &quot;model&quot; select HTML control


&nbsp;&nbsp;&nbsp; $('#model').on('change', function () {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; var selectedModel = $(this).val();






&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; //if
selected other than default option, make a AJAX call to server


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; if (selectedModel !== &quot;-1&quot;) {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $.post('/CascadingDropDownSample/GetSampleColors',


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
{ selectedModel: selectedModel },


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; function (data) {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
cascadingDropDownSample.resetColors();


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
cascadingDropDownSample.getSampleColorsSuccess(data);


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; });


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; else {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; //reset
the colors dropdown


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
cascadingDropDownSample.resetColors();


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }


&nbsp;&nbsp;&nbsp; });


});






//
Module for CascadingDropDownSample containing JS helper functions


function CascadingDropDownSample() {


&nbsp;&nbsp;&nbsp; this.resetCascadingDropDowns = function () {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; this.resetModels();


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; this.resetColors();


&nbsp;&nbsp;&nbsp; };






&nbsp;&nbsp;&nbsp; this.getSampleModelsSuccess = function (data) {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; //binding
JSON data received to HTML select control


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $.each(data, function (key, textValue) {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;$('#model').append($('&lt;option /&gt;', { value: key, text: textValue }));


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; });


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $('#model').attr('disabled', false);


&nbsp;&nbsp;&nbsp; };






&nbsp;&nbsp;&nbsp; this.getSampleColorsSuccess = function (data) {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; //binding
JSON data received to HTML select control


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $.each(data, function (key, textValue) {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $('#color').append($('&lt;option /&gt;', { value: key, text: textValue }));


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; });


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $('#color').attr('disabled', false);


&nbsp;&nbsp;&nbsp; };






&nbsp;&nbsp;&nbsp; this.resetModels = function () {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $('#model
option').remove();


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $('#model').append($('&lt;option /&gt;', { value: '-1', text: 'Please select a
model' }));


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $('#model').attr('disabled', 'disabled');


&nbsp;&nbsp;&nbsp; };






&nbsp;&nbsp;&nbsp; this.resetColors = function () {


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $('#color
option').remove();


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $('#color').append($('&lt;option /&gt;', { value: '-1', text: 'Please select a
color' }));


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $('#color').attr('disabled', 'disabled');


&nbsp;&nbsp;&nbsp; };


}



</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">$(</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">function</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
 () { </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">var</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> cascadingDropDownSample =
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">new</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> CascadingDropDownSample();
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">//binding change event of the &quot;make&quot; select HTML control</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span>$(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'#make'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">).on(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'change'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">function</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> () {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">var</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> selectedMake = $(</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">this</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">).val();
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">//if selected other than default option, make a AJAX call to server</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">if</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> (selectedMake !==
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;-1&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">) {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>$.post(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'/CascadingDropDownSample/GetSampleModels'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>{ selectedMake: selectedMake }, </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">function</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> (data) {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>cascadingDropDownSample.resetCascadingDropDowns(); </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>cascadingDropDownSample.getSampleModelsSuccess(data); </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>}); </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>} </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">else</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">//reset the cascading dropdown</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>cascadingDropDownSample.resetCascadingDropDowns(); </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>} </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span>}); </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">//binding change event of the &quot;model&quot; select HTML control</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span>$(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'#model'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">).on(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'change'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">function</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> () {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">var</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> selectedModel = $(</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">this</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">).val();
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">//if selected other than default option, make a AJAX call to server</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">if</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> (selectedModel !==
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">&quot;-1&quot;</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">) {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>$.post(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'/CascadingDropDownSample/GetSampleColors'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;</span><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>{ selectedModel: selectedModel }, </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">function</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> (data) {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>cascadingDropDownSample.resetColors(); </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>cascadingDropDownSample.getSampleColorsSuccess(data); </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>}); </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>} </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">else</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">//reset the colors dropdown</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>cascadingDropDownSample.resetColors(); </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>} </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span>}); </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">});
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">// Module for CascadingDropDownSample containing JS helper functions</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">function</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> CascadingDropDownSample() {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">this</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">.resetCascadingDropDowns =
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">function</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> () {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">this</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">.resetModels();
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">this</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">.resetColors();
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span>}; </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">this</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">.getSampleModelsSuccess =
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">function</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> (data) {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">//binding JSON data received to HTML select control</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>$.each(data, </span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">function</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> (key, textValue) {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span><span style="">&nbsp;</span>$(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'#model'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">).append($(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'&lt;option
 /&gt;'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">, { value: key, text: textValue }));
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>}); </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>$(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'#model'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">).attr(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'disabled'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">false</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span>}; </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">this</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">.getSampleColorsSuccess =
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">function</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> (data) {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:green; background:white">//binding JSON data received to HTML select control</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>$.each(data, </span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">function</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> (key, textValue) {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>$(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'#color'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">).append($(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'&lt;option
 /&gt;'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">, { value: key, text: textValue }));
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>}); </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>$(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'#color'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">).attr(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'disabled'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">false</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span>}; </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">this</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">.resetModels =
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">function</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> () {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>$(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'#model option'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">).remove();
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>$(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'#model'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">).append($(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'&lt;option
 /&gt;'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">, { value:
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'-1'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">, text:
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'Please select a model'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> }));
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>$(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'#model'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">).attr(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'disabled'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'disabled'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span>}; </span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"></span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span></span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">this</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">.resetColors =
</span><span style="font-size:9.5pt; font-family:Consolas; color:blue; background:white">function</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> () {
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>$(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'#color option'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">).remove();
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>$(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'#color'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">).append($(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'&lt;option
 /&gt;'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">, { value:
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'-1'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">, text:
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'Please select a color'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"> }));
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span>$(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'#color'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">).attr(</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'disabled'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">,
</span><span style="font-size:9.5pt; font-family:Consolas; color:#A31515; background:white">'disabled'</span><span style="font-size:9.5pt; font-family:Consolas; color:black; background:white">);
</span></p>
<p class="MsoNormal" style="margin-bottom:0in; margin-bottom:.0001pt; line-height:normal; text-autospace:none">
<span style="font-size:9.5pt; font-family:Consolas; color:black; background:white"><span style="">&nbsp;&nbsp;&nbsp;
</span>}; </span></p>
<p class="MsoNormal"></p>
<hr>
<div><a href="http://go.microsoft.com/?linkid=9759640" style="margin-top:3px"><img alt="" src="http://bit.ly/onecodelogo">
</a></div>
