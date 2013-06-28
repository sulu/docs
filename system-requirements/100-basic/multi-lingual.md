[index]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/ "Index"
[label_100]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic "100 Basic"
[package_1100]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/caching.md "1100 Caching Mechanisms"
[package_1150]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/url-management.md "1150 URL Management"
[package_1200]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/structure.md "1200 Content Structure"
[package_1250]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/multi-portal.md "1250 Multi-portal Capability"
[package_1300]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/multi-lingual.md "1300 Multi-lingual Capability"
[package_1350]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/workflow.md "1350 Workflow Management"
[package_1400]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/publication.md "1400 Publication"
[package_1450]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/sem-seo.md "1450 SEM/SEO Support"
[package_1500]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/search.md "1500 Search"
[package_1550]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/interfaces.md "1550 Data Interfaces"
[package_1600]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/security.md "1600 Security"
[package_1650]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/image-handling.md "1650 Image Handling"
[package_1700]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/100-basic/usability.md "1700 Usability"
[label_200]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/200-settings "200 Settings"
[label_300]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/300-portals "300 Portals"
[package_3500]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/300-portals/forms.md "3500 Forms"
[label_400]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/400-assets "400 Assets"
[label_500]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/500-contacts "500 Contacts"
[label_600]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/600-global "600 Global"
[label_700]: https://github.com/massiveart/sulu-docs/tree/master/system-requirements/700-dashboard "700 Dashboard"

> [100 Basic][label_100]

###1300 Multi-lingual Capability
####FR-1301 IP to Location
The IP-to-location function automatically forwards the user to the language version of his country of origin. Sulu has to support an IP-to-location service, implemented as a plugin. The mapping of the country-specific IP-address ranges to the different languages can be done by system engineers. A user interface for content managers has do be planned for later versions.  
####FR-1302 Language fall back
A user must be able to choose a different language for a page within the specific language version of a portal. All pages within a content node has to be viewable as list showing all available and assigned languages. The language fall back function has to be accessible also via the list view. 
####FR-1303 Copying a language version
An existing page in a certain language can be a valuable input for the translation into another language. Therefore the user copies a specific page and translates the content. Translated pages can be stored anywhere in the same or in a different portal. The list view allows to copy and save whole nodes or a selection of pages at once.

<table>
    <tr>
        <td colspan=2><b>Related specification documents</b></td>
    </tr>
     <tr>
        <td><i>Name</i></td>
        <td><i>Decription</i></td>
    </tr>
    <tr>
        <td>
        <a href="www.">UC110: Copy language version<br>
        <a href="www.">UC120: xxx
        </td>
        <td>
        Including copying of multiple sites<br>
        xxx
        </td>
    </tr>
     <tr>
        <td>
        <a href="www.">DET103: Multi-lingual Capabilities
        </td>
        <td>
        xxx
        </td>
    </tr>
</table>
