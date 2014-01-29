## DET-003 Form Generation

#### Description

Form generation uses Twig to render [template-structure](https://github.com/sulu-cmf/docs/blob/master/detail-specification/300-portal/DET-301-template-architecture.md) specific Form. 

#### Component diagram
![Form Generation component diagram](https://raw.github.com/sulu-cmf/docs/master/detail-specification/images/diagrams/form-generation.png)

#### Process

1. TemplateController::contentAction -> getStructure from StructureManager with a given key and renders content.html.twig
2. content.html.twig -> foreach Property get(Content)Type
3. content.html.twig -> if isMultiple goto 3.1 else 3.2
	1. include multiple.html.twig with property and type
		1. multiple.html.twig -> include contentType template minOccurs (from template xml) times
		2. multiple.html.twig -> if needsAddButton include add_button.html.twig with property else nothing
	2. include single.html.twig with property and type
		1. single.html.twig -> include contentType template
