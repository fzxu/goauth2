goauth2
=======

Tested for Google, Facebook and Weibo.com. They work perfect.

To use it:

`go get github.com/arkxu/goauth2/oauth`

The change is based on weibo.com's defect about the callback which has `Content-Type: text/plain` in the header but has json format in the body.
They should send application/json content-type instead.

Have to fork my own until Weibo.com correct the problem.

Forked from http://code.google.com/p/goauth2/
