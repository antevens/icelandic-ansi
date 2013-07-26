icelandic-ansi
==============

Icelandic ANSI Keyboard Layout

Steps to modify your keyboard on Linux

1. Edit the file /usr/share/X11/xkb/symbols/is and add the following section to the end of the file: (sudo gedit /usr/share/X11/xkb/symbols/is/)
// Icelandic layout for US 102 key keyboards missing the | < > button next to the Z
// Instead these keys are also mapped to alt-gr  and , . þ
partial alphanumeric_keys
xkb_symbols "102" {
    name[Group1]= "Iceland - 102 keys";

    include "is(basic)"
    key <AB08>  { [   comma,    semicolon,      less,   multiply ] };
    key <AB09>  { [  period,    colon,          greater,        division ] };
    key <AB10>  { [   thorn,    THORN,          bar,    dead_abovedot ] };
};

2. Edit the file /usr/share/X11/xkb/rules/evdev.xml , find the Icelandic section and after the variant Dvorak add a new variant called 102 like so (sudo gedit usr/share/X11/xkb/rules/evdev.xml)
    <variant>
        <configItem>
            <name>102</name>
            <description>102 Key keyboards</description>
        </configItem>
    </variant>

3. Edit the file /usr/share/X11/xkb/rules/evdev.lst , find the is section and add the is: 102 section so that it looks like the following (sudo gedit /usr/share/X11/xkb/rules/evdev.lst):
  Sundeadkeys     is: Sun dead keys
  nodeadkeys      is: Eliminate dead keys
  mac             is: Macintosh
  dvorak          is: Dvorak
  102             is: 102

4. Configure the system to use the new variant, change the default variant by editing the file /etc/default/console-setup (sudo gedit /etc/default/console-setup)
Add the variant by changing the XKBVARIANT variable to "102" so that the config looks like the following:
XKBMODEL="pc105"
XKBLAYOUT="is"
XKBVARIANT="102"
XKBOPTIONS=""
