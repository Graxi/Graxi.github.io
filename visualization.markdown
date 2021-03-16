---
layout: page
permalink: /visualization/
title: Visualization
---

<div id='main'>
	<ul class='post-list'>
		{% assign sorted_posts = site.categories['Visualization'] | sort: 'date' %}
		{% for post in sorted_posts reversed %}
		  <li>
		  	<div class='post-header'>
		  		<div class='post-meta'>
		  			Posted on <time>{{post.date | date: '%B %d, %Y'}}</time>
		  		</div>
		  	  <h1 class='post-title'><a href="{{post.url}}">{{post.title}}</a></h1>
		    </div>
		  	<div class='post-content'>
		    	<div class='post-text'>
		    		{{post.excerpt}}<a class='more-link' href="{{post.url}}"><span></span>(more…)</a>
		    	</div>
		    </div>
		  </li>
		{% endfor %}
	</ul>
</div>