# Deploy Precompiled Blazor WebAssembly Apps to GitHub Pages
> Please view the live demo at https://arvinboggs.github.io/BlazorGitHubPagesDemo

1. Open Visual Studio 2022 (or later).
2. Create a new project.
3. Choose **Blazor WebAssembly App** as the project type.
4. On the **Additional Information** page, tick the **Progressive Web Application** checkbox.  
>This is important so Visual Studio will include the necessary files needed to make your page reload offline.
5. After creating the project, open the **wwwroot\index.html** file and delete the line that has the following code: `<base href="/" />`.  Including this line will make all relative URL's base to the root of the subdomain. [More info][1]. 
> GitHub Pages have URL's in the format of https://\<*username*>.github.io/\<*repository name*>. So, if your GitHub Page URL is https://my_username.github.io/MyRepository, requests to myScript.js, for example, will be fetched from https://my_username.github.io/myScript.js --- which is not what we wanted. We want it to be fetched from https://my_username.github.io/MyRepository/myScript.js.
6. Add a file named **.gitattributes** to the root of your project. Add the following content to the file:
``` text
# put these in .gitattributes file
*.js binary
*.json binary
*.css binary
*.html binary
```
> This is needed because line endings are converted to Unix style when you commit source files like js, json, css, & html. [More info][2]. And we need to push source files without any modification.
7. Add a file named **.nojekyll** to the root of your project.
> This is needed to prevent Jekyll from processing your files, including your directories that start with underscore. [More info][3].
8. `Publish` your project by running the following at the root directory of your project: 
`dotnet publish --configuration Release`
10. `Push` everything in the *\bin\Release\net6.0\publish\wwwroot* directory to your repository.
> Optionally, exclude these files since GitHub have their own compression. 
>- \_framework\*.br
>- \_framework\*.gz
10. Done. Your website is now live.


[1]:https://developer.mozilla.org/en-US/docs/Web/HTML/Element/base
[2]:https://docs.github.com/en/get-started/getting-started-with-git/configuring-git-to-handle-line-endings
[3]:https://github.blog/2009-12-29-bypassing-jekyll-on-github-pages/