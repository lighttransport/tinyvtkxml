# TinyVTKXML

Tiny but powerful VTK XML parser written in C++.
`TinyVTLXML` can parse binary element(`<AppendedData>` tag: http://www.vtk.org/Wiki/VTK_XML_Formats ).

## TODO

* [ ] Support zlib compression of binary data.

## Example


```
#include <cstdio>

#include "tiny_vtkxml.h"

int main(int argc, char *argv[]) {
  lte::tinyvtkxml::TinyVTKXML xml("sample.vti");
  if (xml.Parse()) {
    fprintf(stderr, "Parsing failed.\n");
  }

  std::vector<lte::tinyvtkxml::Node*> data_arrays =
    xml.GetRoot()
    ->FindChild("ImageData")
    ->FindChild("Piece")
    ->FindChild("CellData")
    ->FindChildren("DataArray");

  fprintf(stderr, "size of DataArray: %lu\n", data_arrays.size());
  for (int i = 0; i < data_arrays.size(); ++i) {
    fprintf(
        stderr,
        "In %d th DataArray, appended data starts from %llu with length %u\n",
        i, data_arrays[i]->GetPosition(), data_arrays[i]->GetLength());
  }

  return 0;
}
```

## License

3-clause BSD.
