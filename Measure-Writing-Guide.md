# Output Attributes

We have seen how to output human readble messages from measures.  These messages are useful when running and debugging measures manually using PAT.  However, there is also a need to output machine readable attributes that can be used to create reports about design alternatives in parametric studies.  Each attribute will be associated with the measure that generated it in the workflow. The registerValue method is used to register key value pairs:

```ruby
# runner.registerValue(key,value,units)
runner.registerValue("total_life_cycle_cost",total_life_cycle_cost,"$")
```

The key and units parameters must be strings, the value passed to registerValue can be a double, bool, int, or string.  *Nick, we probably need a way to do nil too right?*

By default, all measure arguments are automatically output in machine readable format.  For example, if a measure takes an argument named 'rotation':

```ruby
relative_building_rotation = OpenStudio::Ruleset::OSArgument::makeDoubleArgument("rotation",true)
```

an attribute named 'rotation' will automatically be added to the measure's output with the value passed in by the user.  Measure writers can output any attributes that they want to.  If a measure outputs multiple attributes with the same name, the last attribute reported by that name will be preserved.  Measure writers are encouraged to use terms that are present in the BCL taxonomy to allow applications to understand attribute names.  Additionally, special modifiers can be added to attribute names which will imply additional relationships between attributes.  These special attribute modifiers are documented below, using the 'rotation' attribute. *Nick, do we need to indicate that rotation is coming from the model as opposed to user input?  Something like model_rotation_intial vs rotation?*

| Modifier | Example | Meaning |
|---|---|---|
|*_initial| rotation_initial|  The value of 'rotation' in the initial model before the measure was run|
|*_final| rotation_final|  The value of 'rotation' in the final model after the measure was run. *Nick, if the measure returns either false or NA without altering the model does it still need to register a "(_final" attribute for every "*_initial" attribute?  This might be a pain if multiple paths return from the measure but I can see the desire to have this.|