# Enhanced Schema for MARCXML

Based on the official (MARC 21 XML Schema)[https://www.loc.gov/standards/marcxml], this schema adds some additional elements to support error handling and fixed-length field decoding.

## Fixed-length Field Decoding

This scheme includes elements for use in `controlfield` elements that can be used for decoding the fixed-length field positions into human-readable values.

```
<controlfield tag="008">
  <encoded>071120s15310406gw a          000 0 lat d</encoded>
  <decoded>
    <field position="00-05" type="Date entered on file">2007-11-20</field>
    <field position="06-14" type="Dates">
      <desc code="s">Single known date/probable date</desc>
      <dated when="1531">1531</dated>
    </field>
    <field position="15-17" type="Place of publication, production, or execution">Germany</field>
    <field position="18-21" type="Illustrations">
      <item>Illustrations</item>
    </field>
    <field position="22" type="Target audience">No attempt to code</field>
    <field position="23" type="Form of item">No attempt to code</field>
    <field position="24-27" type="Nature of contents">No attempt to code</field>
    <field position="28" type="Government publication">No attempt to code</field>
    <field position="29" type="Conference publication">Not a conference publication</field>
    <field position="30" type="Festschrift">Not a festschrift</field>
    <field position="31" type="Index">No index</field>
    <field position="33" type="Literary form">Not fiction (not further specified)</field>
    <field position="34" type="Biography">No attempt to code</field>
    <field position="35-37" type="Language">Latin</field>
    <field position="38" type="Modified record">No attempt to code</field>
    <field position="39" type="Cataloging source">Other</field>
  </decoded>
</controlfield>
```

  | Element | `<encoded>` |
  | :-- | :-- |
  | Purpose | Contains the raw value of the control field. |
  | Attributes | None |
  | May contain |	Empty element |
  
  | Element | `<decoded>` |
  | :-- | :-- |
  | Purpose | Wrapper for the decoded value of the positions withing a fixed-length control field. |
  | Attributes | None |
  | May contain |	`<field>` |
  
  | Element | `<field>` |
  | :-- | :-- |
  | Purpose | Contains the human-readable translations of the position indicated. |
  | Attributes | @position, @type |
  | May contain |	**List:** `<item>`<br />**Dates:** `<dated>`, `<desc>` |

  | Element | `<item>` |
  | :-- | :-- |
  | Purpose | When the position contains a list of values, each value is wrapped in this element. |
  | Attributes | None |
  | May contain | Empty element |
  
  | Element | `<dated>` |
  | :-- | :-- |
  | Purpose | Exclusively for use with Date1/Date2 positions, contains a human-readable date label. |
  | Attributes | @when, @from, @to |
  | May contain | Empty element |
  | Note | Attributes @from and @to are paired together when a range is denoted,<br/>otherwise @when is used for a single year or detailed date. |
  
  | Element | `<desc>` |
  | :-- | :-- |
  | Purpose | Exclusively for use with Type of Date position, contains the human-readable value of position. |
  | Attributes | @code |
  | May contain | Empty element |

## Error Handling

This scheme includes an `<error>` element that can be used to record data quality issues or other errors that were encountered when generating the MARCXML record from a MARC BLOB.

```
<errors>
  <error tag="008">Review the encoded date (06-14)</error>
</errors>
```
 
  | Element | `<errors>` |
  | :-- | :-- |
  | Purpose | Wrapper for `<error>` elements. |
  | Attributes | None |
  | May contain |	`<error>` |
  
  | Element | `<error>` |
  | :-- | :-- |
| Purpose | Record data quality issues with the MARC record that were encounter during validation. |
| Attributes | @tag, @subfield, @indicator |
| May contain |	Empty element |
