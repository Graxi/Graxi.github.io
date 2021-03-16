---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---

<div id='main'>
	<ul class='post-list'>
		{% assign sorted_posts = site.posts | sort: 'date' %}
		{% for post in sorted_posts reversed %}
		  <li>
		  	<div class='post-header'>
		  		<div class='post-meta'>
		  			Posted on <time>{{post.date | date: '%B %d, %Y'}}</time>
		  		</div>
		  	  <h2 class='post-title'><a href="{{post.url}}">{{post.title}}</a></h2>
		    </div>
		    <div class='post-content'>
		    	{% if post.image %}
			    	<div class='post-image'>
			    		<img src="/assets/featured_images/{{post.image}}" />
			    	</div>
		    	{% endif %}
		    	<div class='post-text'>
		    		{{post.excerpt}}<a class='more-link' href="{{post.url}}"><span></span>(more…)</a>
		    	</div>
		    </div>
		  </li>
		{% endfor %}
	</ul>
</div>
<aside>
<!-- 	<div id='categories'>
		<h3>Categories</h3>
		<ul>
			{}
		</ul>
	</div> -->
</aside>