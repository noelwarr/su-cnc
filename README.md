su-cnc
======

Basic CNC API for SketchUp.  Not even work in progress.  This readme is to help me keep track of the general approach I 
plan on taking when writing this extension.

PersistantObject
================
A persistant object is meant to tie the following together

+ Ruby objects
+ SketchUp entities
+ Attribute dictionaries

Here is some pseudo code to illustrate how they work

    class Foo < PersistantObject
      def initialize(entities)
        super
        #construct some geometry and add to the entities
      end
    end
    
    ents = Sketchup.active_model.entities
    foo = Foo.new(ents)
    
    foo["my_data"] = "something interesting"
    
    ent = ents[0]
    obj = Foo.load(ent)
    puts obj.is_a?(Foo) #=>true
    puts obj["my_data"] #=>"something interesting"
    
Tree
====
A helper to iterate through the tree of the model, group or component instance to find persistant objects

    model = Sketchup.active_model
    puts Tree.find(Foo, model) #=> [foo, foo, foo]

Main classes and modules
========================
+ Workpiece (Persistant Object)
+ Operation (Persistant Object)
  + Toolpath (Persistant Object)
  + Hole (Persistant Object)
+ Machine
+ Parser
+ Job
+ Simmulation

General workflow
================
+ Workpiece is defined.  Design is double nested
+ Basic tool for defining toolpaths
+ Basic tool for defining holes
+ Parse
+ Simmulate
