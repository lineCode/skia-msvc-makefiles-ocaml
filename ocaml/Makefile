skia_stubs.obj: skia_stubs.c
	cl /nologo /c /I ../esy-skia /I $(shell ocamlc -where) $<

dllskia_stubs.so: skia_stubs.c
	ocamlmklib  -o  skia_stubs  $<

main.mli: main.ml
	ocamlc -i $< > $@

main.cmi: main.mli
	ocamlc -c $<

main.cmo: main.ml main.cmi
	ocamlc -c $<

main.cma:  main.cmo  dllskia_stubs.so
	ocamlc -a  -o $@  $<  -dllib -lskia_stubs

main.cmx: main.ml main.cmi
	ocamlopt -c $<

main.cmxa:  main.cmx  dllskia_stubs.so
	ocamlopt -a  -o $@  $<  -cclib -lskia_stubs -verbose

myapp.exe: skia_stubs.obj main.cmx
	ocamlopt -o $@ ../esy-skia/out/Static/skia.lib skia_stubs.obj main.cmx

clean:
	rm -f *~ *.[oa] *.so *.cm[ixoa] *.cmxa *.obj *.dll *.exe *.lib
