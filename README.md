# Componolit Ada Style Guide

## Identifiers

### Casing

Identifiers use `Mixed_Case_With_Underscores`. Acronyms remain upper case:

```Ada
Variable_Name : Integer;
Variable_With_TLA : Integer;
```

## Aspects and Pragmas

Wherever possible aspects should be used. Pragmas should only be used if
there is no equal aspect or if using the aspect would cause a bug in the
toolchain.

## Package

### Specification

```Ada
package Foo is
   <declarations>
end Foo;
```

```Ada
package Foo with
  SPARK_Mode,
  Pure
is
   <declarations>
end Foo;
```

### Body

```Ada
package body Foo with
  SPARK_Mode,
  Pure
is
   <declarations>
begin
   <statements>
end Foo;
```

```Ada
package body Foo is
   <declarations>
begin
   <statements>
end Foo;
```

## Subprograms

### Specification

#### Procedure

```Ada
procedure Foo (A : Natural;
               B : Natural) with
  Pre  => True,
  Post => True;
```

#### Function

```Ada
function Bar (A : Natural;
              B : Natural) return Natural with
  Pre  => True,
  Post => True;
```

#### Operator

```Ada
function "+" (Left, Right : Integer) return Integer with
   Pre  => True,
   Post => True;
```

```Ada
function "+" (Left : Integer; Right : Boolean) return Integer with
   Pre  => True,
   Post => True;
```

### Body

#### Procedure

```Ada
procedure Foo is
   <declarations>
begin
   <statements>
end Foo;
```

```Ada
procedure Foo (A : Natural;
               B : Natural) with
  Pre  => True,
  Post => True
is
   <declarations>
begin
   <statements>
end Bar;

```

#### Function

```Ada
function Bar return <type_name> is
   <declarations>
begin
   <statements>
end Bar;
```

```Ada
function Bar (A : Natural;
              B : Natural) return Natural with
  Pre  => True,
  Post => True
is
   <declarations>
begin
   <statements>
end Bar;
```

```Ada
function Bar (N : Natural) return Natural is
  (N + 1)
  with
    Pre => N <= 42;
```

## Types

```Ada
   type Foo_Record is
      record
         Bar : Natural;
      end record
     with
       Convention => C;
```

## If-Conditions

### With one-line condition

```Ada
if <condition> then
   <statements>
end if;
```

### With multi-line condition

```Ada
if
   (((<condition>
     and then <condition>)
    or else <condition>)
   and then <condition>)
then
   <statements>
end if;
```

### If-expressions

```Ada
(if <condition> then <expression> else <expression>)
```

If `<condition>` or one of the `<expression>`s do not fit onto one line:

```Ada
(if <condition>
 then <expression>
 else <expression>)
```

### Case-expressions

```Ada
(case <selector>
 when <alternative> => <expression>,
 when <alternative> => <expression>,
 when others        => <expression>)
```

If at least one `<expression>` does not fit onto the line, *all* lines are wrapped and arrows are *not* aligned:

```Ada
(case <selector>
 when <alternative> =>
    <expression>,
 when <alternative> =>
    <expression>,
 when others =>
    <expression>)
```

## Loops

Conditions in loops are formatted equally to conditions in if expressions.

### While loops

```Ada
while <condition> loop
   <statements>
end loop;
```

With multi line conditions:

```Ada
while
   (((<condition>
     and then <condition>)
    or else <condition>)
   and then <condition>)
loop
   <statements>
end loop;
```

### For loops

```Ada
for <index> in <range> loop
   <statements>
end loop;

for <element> of <array> loop
   <statements>
end loop;
```

For long ranges and arrays that do not fit on a line:

```Ada
for <index> in
   First .. Last
loop
   <statements>
end loop;

for <index> in
   Long_First
   .. Long_Last
loop
   <statements>
end loop;

for <element> of
   Array (First .. Last)
loop
   <statements>
end loop;

for <element> of
   Array (Long_First
          .. Long_Last)
loop
   <statements>
end loop;
```

### Exit conditions

```Ada
loop
   <statements>
   exit when <condition>;
   <statements>
   exit when (((<condition>
               and then <condition>)
              or else <condition>)
             and then <condition>);
   <statements>
end loop;
```

## Declarations

```Ada
procedure Foo (Buffer_Address : System.Address;
               Buffer_Length  : Interfaces.C.Size_T)
is
   Buffer : Array_Type (Index_Type'First ..
                        Index_Type'First + Length_Type (Buffer_Length) - 1) with
     Address => Buffer_Address;
begin
   <statements>
end Foo;
```

## Use-clauses

Use clauses for packages are *not* permitted. Use clauses for types should be as limited in scope as feasible.
