### convert log into html

```
# same file
sed -i '1i\<pre>' scpcss0
sed -i '$a</pre>' scpcss0

# new file
sed '1i\<pre>' scpcss0 > output.html
sed -i '$a</pre>' output.html
```

<a href="#top">Back to top</a>
