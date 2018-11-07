# Project 7 - WordPress Pentesting

Time spent: 5 hours spent in total

> Objective: Find, analyze, recreate, and document **three vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. WordPress 3.3-4.7.4 - Large File Upload Error XSS
  - [ ] Summary: This vulnerability allows someone to add malicious script into a filename.  If said file is uploaded onto wordpress, an XSS appears inside the administrator's control panel.  Two different "file to large" cases end up in interpolating the file name and appending it into DOM unsanitized leading to XSS.
    - Vulnerability types:XSS
    - Tested in version: 4.2
    - Fixed in version: 4.7.5
  - [ ] GIF Walkthrough: homework1.gif 
  - [ ] Steps to recreate: First, you must download a file that exceeds the 2 MB limit WordPress has.  Rename this file to Dinosaurs secret life<img src=x onerror=alert(1)>.png.  Attempt to upload this file onto WordPress. An alert box will appear with the working XSS exploit.
  - [ ] Affected source code: image file name, image file must exceed 2 MB
    - [Link 1](https://hackerone.com/reports/203515)
    
2. WordPress  4.0-4.7.2 - Authenticated Stored Cross-Site Scripting (XSS) in YouTube URL
  - [ ] Summary: An attacker can insert malicious Cross-Site Scripting by editing code into YouTube URL links on WordPress.  The link will be shortened down to the embedded YouTube URL.  Even though it is not shown, the Cross-Site Script will pass through the website as a working XSS exploit.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Fixed in version: 4.7.2
  - [ ] GIF Walkthrough: homework2.gif 
  - [ ] Steps to recreate: In the comments section of a page, insert the malicious URL, https://youtube[.]com/watch?v=abc<svg onload=alert(1)>.  After posting the comment, an error message will appear whenever loading or reloading the page.
  - [ ] Affected source code: https://youtube[.]com/watch?v=abc<svg onload=alert(1)>
    - [Link 1](https://blog.sucuri.net/2017/03/stored-xss-in-wordpress-core.html)
  
3. WordPress 2.5-4.6 - Authenticated Stored Cross-Site Scripting via Image Filename
  - [ ] Summary: An attacker can manipulate an image file name with a Cross-Site Scripting payload.  If said image is uploaded, Wordpress will use the file name as the image title on attachment pages.   
    - Vulnerability types:XSS
    - Tested in version:4.2
    - Fixed in version: 4.6.1
  - [ ] GIF Walkthrough: homework3.gif
  - [ ] Steps to recreate: Download any image and rename it to cengizhansahinsumofpwn<img src=a onerror=alert(document.cookie)>.jpg.  After uploading the image onto WordPress, go to the attachment page.  The file name will be the same as the title of the attachment page.  With the Cross-Site Script that was used as our image file name, a pop up box will appear once the page is loaded.
  - [ ] Affected source code: image file name
    - [Link 1](https://sumofpwn.nl/advisory/2016/persistent_cross_site_scripting_vulnerability_in_wordpress_due_to_unsafe_processing_of_file_names.html)

## Assets

None

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Many comment Cross-Site Scripts did not work due to WordPress inserting a NoFollow code into the scripts. No plugins would resolve the issue.

## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
