# Project 7 - WordPress Pentesting

Time spent: **5** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

### 1. WordPress <= 5.2.3 - Unauthenticated View Private/Draft Posts
  - [ ] Summary: Allows an unauthenticated user to view private or draft posts
    - Vulnerability types: Privilege Escalation
    - Tested in version: 4.2
    - Fixed in version: 4.2.25
  - [ ] GIF Walkthrough: <img src="Vulnerability1.gif">
  - [ ] Steps to recreate: 
       - create a post and save it as a draft or make it private.
       - log out or use an incognito browser, in the browser type in the URL: `http://wpdistillery.vm/?static=1&order=asc`
  - [ ] Affected source code:
    - [Link 1](https://github.com/WordPress/WordPress/commit/f82ed753cf00329a5e41f2cb6dc521085136f308)
    - [Link 2](https://0day.work/proof-of-concept-for-wordpress-5-2-3-viewing-unauthenticated-posts/)

    
### 2. WordPress <= 4.2 - Unauthenticated Stored Cross-Site Scripting (XSS)
  - [ ] Summary: Allows injection of arbitrary web script or HTML within a comment that exceeds 64 kb. 
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.1
  - [ ] GIF Walkthrough: <img src="vulnerability2.gif">
  - [ ] Steps to recreate: 
       - Post a comment on the site that includes the script `<a title='x onmouseover=alert(unescape(/got%20you/.source))          style=position:absolute;left:0;top:0;width:5000px;height:5000px  AAAAAAAAAAAA...[64 kb]..AAA'></a>` The '..AAAA..' portion of the script must exceed 64 kb.
       - Refresh the page or move your mouse and you will see the alert. This can be recreated as a visitor.
  - [ ] Affected source code:
    - [Link 1](http://klikki.fi/adv/wordpress2.html)
    
### 3. WordPress <= 4.2.2 - Authenticated Stored Cross-Site Scripting (XSS)
  - [ ] Summary: Allows a user with the role of Author or contributor to create posts or pages that contain malicious script.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.3
  - [ ] GIF Walkthrough: <img src="Vulnerability3.gif">
  - [ ] Steps to recreate: 
       - Convince the admin to create a user account for you with the role of Author or Contributor or if you're lucky, admin.
       - Publish a post or page using your new account and insert the malicious script: `<a href="[caption code=">]</a><a title=" onmouseover=alert('Gotcha!')  ">link</a>` 
  - [ ] Affected source code:
    - [Link 1](https://klikki.fi/adv/wordpress3.html)
    
### 4. WordPress  4.0-4.7.2 - Authenticated Stored Cross-Site Scripting (XSS) in YouTube URL Embeds
  - [ ] Summary: Allows a user with the privileges to create a post or page to upload malicious youtube URL embedded with XSS code.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.13
  - [ ] GIF Walkthrough: <img src="Vulnerability4.gif">
  - [ ] Steps to recreate: 
       - Create a post or page and insert the following script into the body `[embed src='https://youtube.com/embed/12345\x3csvg onload=alert(5678)\x3e'][/embed]`
       - Publish to see the alert
  - [ ] Affected source code:
    - [Link 1](https://blog.sucuri.net/2017/03/stored-xss-in-wordpress-core.html)
    
### 5. WordPress <= 4.2.3 - Widgets Title Cross-Site Scripting (XSS)
  - [ ] Summary: Allows a user with admin privileges to insert malicious script into a widget.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.2.4
  - [ ] GIF Walkthrough: <img src="Vulnerability5.gif">
  - [ ] Steps to recreate: 
       - Log in as admin and navigate to widgets -> add a widget -> text
       - Put in any title then insert the following script into the body `<SCRIPT>alert('BOO!')</SCRIPT>`
       - Publish then navigate to any page on the site to see the alert
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/changeset/33529) 

## Assets
N/A

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Describe any challenges encountered while doing the work

## License

    Copyright [2020] [Xiomara Henriquez]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
