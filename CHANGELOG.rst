Change & Version Information
============================

The following is a summary of changes and improvements to
:mod:`eulxml`.  New features in each version should be listed, with
any necessary information about installation or upgrade notes.


0.21.2
------

* Bug fix: correctly support parameters in
  :meth:`eulxml.xmlmap.XmlObject.xsl_transform`
* Automatically encode string parameter values passed to
  :meth:`~eulxml.xmlmap.XmlObject.xsl_transform` as
  lxml string parameters (:class:`lxml.etree.XSLT.strparam`)

0.21.1
------

* Bug fix: :meth:`eulxml.xmlmap.XmlObject.xsl_transform` now recognizes
  text output as a valid, non-empty XSL result

0.21
----

* Add default unicode output of date value for MODS date fields
  (:class:`~eulxml.xmlmap.mods.Date` and all date variants)
* Bug fix: :class:`~eulxml.forms.XmlObjectForm` now uses the
  field order as defined on the form when updating the XML instance
  (fix for XML where schema requires fields in a specific order)


0.20.3
------

* Revert unused namespace cleanup change to serialization it generates
  less optimal output in certain cases.
* Minor updates to :mod:`~eulxml.xmlmap.eadmap`:

  * Added mapping for `xlink:show` attribute to
    :class:`~eulxml.xmlmap.eadmap.DigitalArchivalObject`
  * Added mapping for `note` field
    :class:`~eulxml.xmlmap.eadmap.Index`
  * Changed :class:`~eulxml.xmlmap.eadmap.Note` paragraph content from
    string list to node list, to support formatting.
  * Added mapping for ``processinfo`` to
   :class:`~eulxml.xmlmap.eadmap.ArchivalDescription` and
   :class:`~eulxml.xmlmap.eadmap.Component`

0.20.2
-------

* Unused namespaces will now be cleaned up before serialization in
  :meth:`eulxml.xmlmap.XmlObject.serialize' and
  :meth:`eulxml.xmlmap.XmlObject.serializeDocument'
* :mod:`eulxml.xmlmap.eadmap` have been updated with root element names
  where possible, to better support using :mod:`~eulxml.xmlmap.eadmap` to
  update or modify EAD documents.

0.20.1
-------

* Adjust :mod:`eulxml.xmlmap` fields for better results when inspected by
  sphinx autodoc or other similar tools.

0.20.0
-------

* Update :mod:`eulxml.xmlmap.mods` with support for id attribute on top-level MODS
  element. Contributed by `bcail <https://github.com/bcail>`_.
* Update :mod:`eulxml.xmlmap.eadmap` with support for digital archival object tags.
* Add :class:`eulxml.xmlmap.fields.DateField` to support date fields
  separately from :class:`eulxml.xmlmap.fields.DateTimeField`; also includes
  minimal support for date fields in :class:`eulxml.forms.xmlobject.XmlObjectForm`.

0.19.1
-------

* Pinned MODS version to 3.4 to guard against new versions of the schema breaking validation

0.19.0
-------

* Corrected a minor bug where schema validation errors were not cleared between
  multiple validations.
* To avoid permission denied warning for auto-generated parser files,
  parsetab files are now created in python tempdir if the running user
  doesn't have write permission in the package installation directory.
  [`Issue 1 <https://github.com/emory-libraries/eulxml/issues/1>`_]
* When an XSLT transformation results in an empty document,
  :meth:`eulxml.xmlap.XmlObject.xsl_transform` now returns None.
  [`Issue 6 <https://github.com/emory-libraries/eulxml/issues/6>`_]
* Development requirements can now be installed as an optional requirement
  of the eulxml package (``pip install "eulxml[dev]"``).
* Unit tests have been updated to use :mod:`nose`
* New functionality in :mod:`eulxml.xmlmap.cerp` for parsing email dates
  and generating CERP xml from a Python email message object.


0.18.0 - Formset Ordering and DateTime
--------------------------------------

* :class:`eulxml.forms.xmlobject.XmlObjectForm` formsets now support
  ``can_order``.
* :class:`eulxml.xmlmap.fields.DateTimeField` is now included in
  available :mod:`eulxml.xmlmap` fields.  This replaces the previously
  officially-unreleased, under-documented and -tested and misnamed
  ``DateField``.  Date-time format handling and whitespace
  normalization contributed by `jheath- <https://github.com/jheath->`_.


0.17.1 - Bugfix Release
-----------------------

* Fixed an error in eulxml.xpath parse that resulted in parse errors
  when other lexers are defined.


0.17.0 - Minor Enhancements
---------------------------

* :class:`eulxml.xmlmap.XmlObject` now supports lazy-loading for XSD
  Schemas.  To take advantage of this feature,
  :class:`~eulxml.xmlmap.XmlObject` subclasses should define an
  ``XSD_SCHEMA`` location but should not set an ``xmlschema``.
* When :ref:`field <xmlmap-field>` mapped on a
  :class:`eulxml.xmlmap.XmlObject` is deleted, any XPath predicates
  that could have been automatically constructed when setting the
  value will be deleted from the :class:`~eulxml.xmlmap.XmlObject`
  where possible, if they are otherwise empty.


0.16.0 - MODS and PREMIS
------------------------

* Add basic support for `MODS <http://www.loc.gov/standards/mods/>`_ in
  :mod:`eulxml.xmlmap.mods`.
* Add basic support for `PREMIS <http://www.loc.gov/standards/premis/>`_ in
  :mod:`eulxml.xmlmap.premis`.
* Minor logging and error handling improvements.

0.15.3 - Minor Enhancement
--------------------------

* Downgrade the lack of an HTTP_PROXY set in the environment from a
  RuntimeError to a Warning with schema validation disabled.

0.15.2 - Bugfix Release
-----------------------

* Fixed an error in the dependency structure that prevented the package from
  being used after installation through PyPI.

0.15.1 - Bugfix Release
-----------------------

* Fixed an error in the dependency structure that prevented the package from
  being installed through PyPI.

0.15.0 - Initial Release
------------------------

* Split out xml-related components (:mod:`~eulxml.xpath`,
  :mod:`~eulxml.xmlmap`, and :mod:`~eulxml.forms`) from :mod:`eulcore`
  into :mod:`eulxml` for easier re-use.
