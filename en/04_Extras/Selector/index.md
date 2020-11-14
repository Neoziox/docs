
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<h3>Selector - custom TV для составления списка документов </h3>
Selector -  custom TV for listing documents in Evolution CMS.
<p>Download here: <i class="fa fa-github fa-lg text-primary"></i> <a href="https://github.com/Pathologic/Selector" rel="nofollow" target="_blank">Pathologic</a></p>
<p>Selector is a replacement for <a href="129.html" title="mm_ddSelectDocuments" target="_blank">mm_ddSelectDocuments</a>.</p>
<p>Unlike mm_ddSelectDocuments:</p>
<ul>
	<li>gets along with SimpleGallery;</li>
	<li>thanks to DocLister, you can select data for the list as you like and from anywhere;</li>
	<li>the list of search results can be designed in any way (implemented using prepare in DocLister);</li>
	<li>the code is completely open (there was a thought to figure out the conflict between mm_ddSelectDocuments and SimpleGallery, but minified js immediately discouraged the desire).</li>
</ul>
<p>The code turned out to be simple, it's not difficult to figure it out if desired.</p>
<p>Requires DocLister to work.</p>
<p>There is nothing more to write about this component, except that the customization process requires some explanations. Let me explain right away with an example.</p>
<p>Let's say there is a tv parameter named <i>related_my_tv</i> to store a list of similar products. To make its behavior different from the base one, you need to create a class in the assets/tvs/selector/lib/related_my_tv.controller.class.php file:</p>
<pre class="brush: php;">
&lt;?php namespace Selector;
include_once(MODX_BASE_PATH.'assets/tvs/selector/lib/controller.class.php');
class RelatedController extends SelectorController {
... //Override what is needed
}
</pre>

<p>In most cases, I think it will be enough to change the dlParams property, which stores the default parameters for running DocLister:</p>
<pre class="brush: php;">
&lt;?php namespace Selector;
include_once(MODX_BASE_PATH.'assets/tvs/selector/lib/controller.class.php');
class Related_my_tvController extends SelectorController {
    public function __construct($modx) {
        parent::__construct($modx);
        $this-&gt;dlParams['parents'] = 5;
        $this-&gt;dlParams['addWhereList'] = 'c.published = 1';
    }
}
</pre>
<p>If this part is not clear, then I can advise you to contact here: <a href="https://bezumkin.ru/training/course3/" rel="nofollow" target="_blank">bezumkin</a></p>
<p>Please note that the parameter is related, the file name is <b>related_my_tv</b>.controller.class.php, and the class name is <b>Related_my_tv</b>Controller (with a capital letter).</p>
<p>You can also load the required class manually using the plugin on OnManagerPageInit. In this case, only the correct class name matters. There is also a restriction on the name of the tv-parameter: only Latin letters and the underscore character are allowed.</p>
