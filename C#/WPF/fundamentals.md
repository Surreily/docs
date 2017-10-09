WPF Introduction
================

WPF is split into several layers:

* **Presentation Framework** - Top level concepts (Control, Layout, etc).
* **Presentation Core** - Public face of composition engine.
* **Composition Engine** - Communicate with DirectX using unmanaged code.
* **DirectX** - Lowest level.

## Pros and Cons

* WPF graphics automatically scale well for higher resolution displays.
* WPF allows flexibility for GUI design (for example, 3D models and buttons overlapping).

## XAML

XAML is not tied to WPF! Generally, it is a language for constructing .NET objects. The following two code chunks are identical.

The following code...

    <Button x:Name="myButton"
            FontSize="24"
            FontFamily="Candara"
            Foreground="DarkRed">
      Click me!
    </Button

...is identical to...

    Button myButton = new Button();
    myButton.FontSize = 24;
    myButton.FontFamily = new FontFamily("Candara");
    myButton.Foreground = Brushes.DarkRed;
    myButton.Content = "Click me!";

### UI Tree

WPF elements contains two views onto the UI structure: the *logical tree* and the *visual tree*. The logical tree is a subset of the visual tree.

### Events and Commands

Events are generally tied to the visual tree.

* **Event Routing** specified the direction of events.
  * **Tunneling** goes from root to children, and continues until it's handled.
  * **Bubbling** goes from children to root, and also continues until it's handled.
* Events often come in pairs: the *preview* event and the *actual* event.

### Commands

Commands allow us to define common application commands, such as printing, saving, or loading.

### Controls

The button control features a *click event*, a *content model*, the *focus*, *commands*, and *automation* for accessibility.

* **Lookless** - it does not know how to render itself.
  * **Templates** are used to "style" the button.

To define a template, we can use *property syntax*: `<class.property>`:

    <Button Background="Green">
    <Button.Template>
      <ControlTemplate TargetType="Button">
        <Rectangle Fill="{TemplateBinding Background}" RadiusX="5" RadiusY="5" />
      </ControlTemplate>
    </Button.Template>

### Content Model

Many elements (such as `Button`) can have a child element, called a content model.

    <Button ... >
      <StackPanel>
        <Ellipse ... />
        <TextBlock>Hello</TextBlock>
        <Ellipse ... />
      </StackPanel>
    </Button>
