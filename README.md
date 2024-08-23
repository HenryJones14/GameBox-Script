# GameBox Script

GameBox Script is a powerful and flexible scripting language designed to organize and manage code within distinct namespaces. This language enforces a strict namespace hierarchy, ensuring that all code is well-structured and free from global pollution. - ChatGPT

## Language syntax

### Namespaces

Namespaces are here to organize code and can be ether **declared** or **included**.

[ `include` | `declare` ] `namespace` \<name\> [ `;` | `{}` ]

All structs, objects and modules need to be in at least one namespace, because there is no global namespace.

Namespaces are per `struct`, `object` or `module`. Meaning that each one of them has a single namespace declaration and some namespace includes (always including its own declaration). This means that you cant have a single `function` in a `module` that uses a different namespace.

Both *declare* and *include* can be used inline and scoped, but inline uses need to come before any structs, objects or modules.

```
include namespace GameEngine:Graphics;
include namespace GameEngine:Input;

declare namespace Application:Game;


// Game enemy code

// Game player code
```

```
include namespace GameEngine:Graphics
{
    include namespace GameEngine:Input
    {
        declare namespace Application:Game
        {
            // Game enemy code
            
            // Game player code
        }
    }
}

```

Both methods can be mixed asswell.

```
include namespace GameEngine:Graphics;

declare namespace Application;


declare namespace Game
{
    // Game enemy code
    
    include namespace GameEngine:Input
    {
        // Game player code
    }
}
```

You should use inline includes and scoped declarations by default.

### Structs

Structs are here to allow you to make custom types. All standard library types are structs. Structs can only contain other structs.

[ `public` | `within` | `member` | `hidden` ] `struct` \<name\> `{}`

### Objects

Objects are here to make use of generics and to allow encapsulation.

[ `public` | `within` | `member` | `hidden` ] `object` \<name\> `{}`

### Modules

Modules are here to make libraries without state.

[ `public` | `within` | `member` | `hidden` ] `module` \<name\> `{}`

### Functions

Functions are here to do the actual code.

[ `public` | `within` | `member` | `hidden` ] `function` \<name\> `(` \<arguments\> `)` `{}` where \<arguments\> is any number of [ `input` | `output` ] \<type\> \<name\>

## Standard library

Standard library is organized into namespaces with no structs, objects and modules in namespaces that contain other namespaces. Only top level namespaces have structs, objects and modules.

### Structs

`sInt16`
`sInt32`
`sInt64`

`uInt16`
`uInt32`
`uInt64`

`sFloat16`
`sFloat32`
`sFloat64`

`sByte8`

`uByte8`

`uBool1`

`uChar8`

`uString8`
