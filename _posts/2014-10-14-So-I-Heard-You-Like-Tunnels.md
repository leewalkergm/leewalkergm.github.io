Recently, I’ve been doing a lot of work with mobile applications and hosted APIs. This has lead to one or two frustrations when trying to test the APIs out on actual devices…

We have an Azure Mobile Service project which links to a Cordova driven mobile application.

I remember stumbling upon this piece of software a few months ago when I was questioning about how to show mobile apps to clients (forgetting that we deployed our web services onto AWS), but I never really got to use it too much or see it’s greater potential.

## What we did
A way I’ve brought this to our workflow is to first, open up my IISExpress instance by adding a new line into my applicationHosts.config file as follows:
```XML
<site name="MvcMusicStore" id="2035164975">
  <application path="/" applicationPool="Clr4IntegratedAppPool">
      <virtualDirectory path="/" physicalPath="C:\Code\MvcMusicStore" />
  </application>
  <bindings>
      <binding protocol="http" bindingInformation="*:59737:localhost" />
      <binding protocol="http" bindingInformation="*:59737:127.0.0.1" />
      <!-- ^this is the new line! -->
  </bindings>
</site>
```
Secondly, I simply point ngrok to my .net WebApi’s 127.0.0.1:59737 url

```
ngrok -subdomain=lee-api-test 127.0.0.1:59737
```
and…

*BOOM!*

We have a WebApi which is exposed to everyone, anywhere in the world and therefore my mobile application!

This saved me so much time that I donated some money to the developer of ngrok and unlocked the premium features of ngrok.

A BIG thanks to Alan Shreve (@inconshreveable) and I highly recommend you check out his blog.

– Lee

ngrok’s site: http://ngrok.com/

Alan Shreve’s site: https://inconshreveable.com/
