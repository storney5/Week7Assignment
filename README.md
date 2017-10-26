# Week7Assignment
Sean Torney

# Project 7 - WordPress Pentesting

Time spent: **6** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. Authenticated Stored Cross-Site Scripting
  - [ ] Summary: An author or contributor of the site could compromise a vulnerability in the site by crafting
				 a malicious HTML script inside a post in the text mode, which the wordpress shortcode compressor
				 would make a dangerous attack. The attack occurs once the admin views the post.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.3
  - [ ] GIF Walkthrough: First_Vulnerability.gif
  - [ ] Steps to recreate: First, I created a new user and granted the new user author authentication.  Then, I
						   logged in as the new author and created a new post. In the post, I inserted: 
						   <a href="[caption code=">]</a><a title=" onmouseover=alert('hacked')  ">link</a>
						   After I published the post, I logged in as the admin and viewed the post and once I 
						   put the cursor over the "link", the xss attack occured.
  - [ ] Affected source code:
    - [Link 1] (https://core.trac.wordpress.org/browser/tags/4.2/src/wp-includes/shortcodes.php)
	- [Link 2] (https://core.trac.wordpress.org/browser/tags/4.2/src/wp-includes/kses.php)
	- [Link 3] (https://core.trac.wordpress.org/browser/tags/4.2/src/wp-admin/post.php)
	
2. Unauthenticated Stored Cross-site Scripting
  - [ ] Summary: A viewer of the webpage can compromse a vulnerability by crafting a malicious HTML script in 
				 a comment to a post.  The attack occurs when the admin views the comment.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.1
  - [ ] GIF Walkthrough: Second_Vulnerability.gif
  - [ ] Steps to recreate: I began by creating a comment on an already published post. In the text box, I 
						   inserted: <a title='x onmouseover=alert(unescape(/hello%20world/.source)) 
						   style=position:absolute;left:0;top:0;width:5000px;height:5000px  AAAAAAAAAAAA...[64 kb]..AAA'></a>
						   I had to put in 64kb of A's in order for the wordpress code to truncate the comment and thus exposing
						   the webpage to the xss attack.
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/4.2/src/wp-comments-post.php)
	
3. Authenticated Shortcode Tags Cross-site Scripting
  - [ ] Summary: An author or contributor can compromise this vulnerability by crafting a malicious HTML script 
				 into a post.  The attack occurs when the admin views the post.  Like the first vulnerability,
				 this attack outsmarts the wordpress shortcode compressor.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.5
  - [ ] GIF Walkthrough: Third_Vulnerability.gif
  - [ ] Steps to recreate: First, I created a new post as an author of the site.  Then, in text mode, I inserted:
						   [caption width="1" caption='<a href="' ">]</a><a href="http://onMouseOver='alert("hacked")'">Click me</a>
						   After publishing, I logged back in as the admin and viewed the post. Once the mouse scrolled over the link,
						   the attack occured.
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/4.2/src/wp-includes/shortcodes.php)

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## License

    Copyright [2017] [Sean Torney]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

