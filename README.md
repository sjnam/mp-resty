TeX graphics in all browsers
=======
An openresty web application for TeX graphics (`metapost`, `graphviz`) that works
in all browsers.

No more setup for readers. It just works.

Synopsis
---------

````html
<html>
<body>

<H1>Metapost</H1>
<mplibcode width="300">
beginfig(1)
  u:=1.3cm; transform T; z1=(0,2u); n:=5;
  for i=1 upto n-1: z[i+1]=z1 rotated (360*i/n);
  endfor;
  z1 transformed T=0.1[z1,z2];
  z2 transformed T=0.1[z2,z3];
  z3 transformed T=0.1[z3,z4];
  path p;
  p = for i=1 upto n: z[i]--endfor cycle;
  for i=0 upto 100:
    fill p withcolor 0.2*white; p:=p transformed T;
    fill p withcolor white;     p:=p transformed T;
  endfor;
endfig
</mplibcode>

<mplibcode src="/source/tree.mp" cache="no"></mplibcode>

<H1>Graphviz</H1>

<graphviz>
digraph G {
    main -> parse -> execute;
    main -> init;
    main -> cleanup;
    execute -> make_string;
    execute -> printf
    init -> make_string;
    main -> printf;
    execute -> compare;
}
</graphviz>

<graphviz src="https://graphviz.org/Gallery/directed/Linux_kernel_diagram.gv.txt"
          cmd="dot"></graphviz>

</body>
</html>
````

Run
---
```bash
#The name of directory "/path/to" can be made by any name as you want.
% git clone https://github.com/sjnam/tex-graphics.git
% cd tex-graphics
% mkdir -p /path/to/playground
$ cp -r playground/* /path/to/playground
% docker build -t mpresty .
% docker run -d -p 8080:8080 \
  -v /path/to/playground:/webapps/playground \
  --name gxn mpresty
% docker start gxn
```

Try to visit the following pages
- http://localhost:8080/gxn/sunflower.html
- http://localhost:8080/gxn/test.html
- http://localhost:8080/preview.html

Create a `sample.html` file with the above [Synopsis](#Synopsis) and put it in the `/path/to/playground/gxn` directory and visit the page http://localhost:8080/gxn/sample.html

Author
------
Soojin Nam, jsunam@gmail.com

License
-------
Public Domain
