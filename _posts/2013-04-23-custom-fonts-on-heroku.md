---
layout: post
title: "Custom fonts on Heroku" 
author: John Beynon
---

We had a requirement to use a specific font when rendering a PDF using
wkhtmltopdf / wicked_pdf.

We've been scratching our heads on this one for a while and had resorted to
thinking that we'd need to use a custom build pack.

It turns out there's a much simpler solution. Ubuntu custom fonts can be added
to the .fonts folder in your home directory. If you drop into a bash session and
try and access the ~ path you get taken to your application. So we thought, hang
on - maybe we can just commit a font to our app by putting it in a .fonts
directoy. It turns out you can!

