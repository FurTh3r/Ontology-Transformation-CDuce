# Ontology Validator and Transformer in CDuce

## Overview
This project provides a set of CDuce functions to load, validate, filter, and transform RDF/XML ontology files. It ensures that the ontology conforms to predefined structural rules and removes invalid elements. If necessary, the ontology is transformed to retain only compatible and valid components.

## Features
- **Safe XML Loading:** Loads RDF/XML files with error handling.
- **Ontology Validation:** Checks if the loaded XML conforms to the expected ontology structure.
- **Filtering Mechanism:** Removes invalid attributes and classes that do not adhere to the ontology definition.
- **Transformation Support:** Attempts to restructure the ontology to maintain valid elements.
- **Output Handling:** Saves the validated/transformed ontology to a file.

## Dependencies
- [CDuce](http://www.cduce.org/): A functional language for XML processing.

## Usage
### Loading and Validating an Ontology
The system loads an ontology file from a specified path and checks its validity.
```cduce
let xml_file = safe_load_xml "INPUT_PATH";;
if (validate_elements xml_file) then
  print "First check: Valid Ontology\n"
else
  print "First check: Not Valid Ontology\n";;
```
### Filtering and Transforming Ontology
If the ontology is invalid, the script attempts to transform it by filtering out non-conforming elements.
```cduce
let valid_ontology = verify_and_transform_ontology xml_file;;
```
### Saving the Processed Ontology
If the ontology is successfully validated or transformed, it is saved to an output file.
```cduce
if (validate_elements valid_ontology) then
  (
    print "Transformed Ontology saved to file\n";
    dump_to_file_utf8 "OUTPUT_PATH" (print_xml_utf8 valid_ontology)
  )
else
  print "Failed to validate or transform ontology\n";;
```
### Example Execution
1. Load an ontology from `ontology.xml`.
2. Validate and transform if necessary.
3. Save the processed ontology to `validated_ontology.xml`.
```shell
cduce -load ontology_validator.cduce
```

## Code Breakdown
### Core Functions
- `safe_load_xml(path : Latin1) : AnyXml`
  - Loads an XML file and handles syntax errors.
- `validate_elements(input : AnyXml) : Bool`
  - Checks if the XML structure conforms to the ontology definition.
- `filter_valid_classes(classes : [ AnyXml* ]) : [ AnyXml* ]`
  - Filters valid ontology classes, removing elements without attributes.
- `transform_compatible_elements(ontology : AnyXml) : AnyXml`
  - Transforms ontology to retain only compatible and valid elements.
- `verify_and_transform_ontology(input : AnyXml) : AnyXml`
  - Validates the ontology and applies transformation if needed.

## Notes
- Ensure that the RDF/XML file follows standard ontology definitions.
- Modify `INPUT_PATH` and `OUTPUT_PATH` in the script for custom file processing.

## License
This project is released under the MIT License.

