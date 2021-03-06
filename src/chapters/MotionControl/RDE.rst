
***********************************
RDE - Robox Development Environment
***********************************

First step
==========

In order  to getting started with the controller, we need a memory card where we have to copy ``RTE`` and some configuration file. A new memory card will have the folder ``KEY`` that is generated by Robox for license.

After the installation of ``RDE``, ``RCE`` and ``Icmap`` we need to copy in the installation folder the license in order to compile programs. The license is provided by Robox.

Before creating a new project, a workspace have to be created. A workspace may contain more than one project. In the menu bar, the workspace menu, allow to open, create and manage workspaces, also to access the predefined examples .

.. _figrde1:
.. figure:: images/rde/rde1.png
    :align: center
    :figwidth: 400px

    RDE main windows


New RTE project
===============


Tools
=====

From the workspace we can access the tools provided by ``RDE``. Different king of tools are provided to debug and monitor the software: panels, oscilloscope, variable monitors and command shell.

.. _figtools:
.. figure:: images/rde/workspace.png
    :align: center
    :figwidth: 400px

    Workspace


Command shell
-------------

The shell allow to interact with the controller via shell commands and device commands.
The most important commands for debugging are ``sysinfo`` to get information about the controller, ``als`` to get the list of alarms in the stack and ``mreport`` to get a report about the activities of the controller, the result is a log menu that can be exported to text file..

We can make shortcuts to the most used commands. Click the mouse right button and go to ``set quick commands`` in order to define shortcuts. A list of defined shortcuts is available from the function keys ``[F1-F12]`` and from the action menu accessible from the mouse right click.

.. _figquickcommands:
.. figure:: images/rde/quickcommands.png
    :align: center
    :figwidth: 400px

    Command shell: Quick commands


There are different types of commands, some types to manage variables others to manage the flash card other the device. A list of commands is available in the official documentation.

We will see some of the most used commands divided by category. Several commands can be used alone or with options. More than one command can be sent together by using the ``\&`` operator. Take a look at :ref:`figquickcommands` in order to see the usage and syntax of some commands.

Variable management
^^^^^^^^^^^^^^^^^^^

``DV``: Display variable value. The dv command allow us to monitor the value of variables e.g. ``dv nvr 1`` display the value of the register ``nvr(1)``.

``SV``: Set variable value

``FV``: Force variable value

``RV``: Release variable value

Device management
^^^^^^^^^^^^^^^^^^^

``adv`` Resets the device alarm

``sysinfo`` Get information on connected device.

``mreport`` It displays the events log. the option ``-a`` display all reports. Other options are available in order to filter the report.

``als`` It displays the contents of the alarms stack.

``swreset`` Request for software reset.

``uar`` Opens a file present in the flash card and refreshes the assignments to  R, NVR, RR, NVRR, SR and NVSR with the current values but leaves the comment lines unchanged.

Flash management
----------------

``fsave`` Save file from flash.

``fview``

Example of use
--------------

	- ``nvr 1 5`` Set the value of nvr register 1 to 5, equivalent to ``sv nvr 1 5``
	- ``nvr 4.2 1`` Set the bit 2 of nvr register 4 to 1
	- ``d inp_w 100``
	- ``d inp 1``
	- ``d nvr 1``
	- ``d nvr 2.3``
	- ``d nvr 1 5`` Displays 5 registers starting from 1
	- ``d nvr 1 5 -v``  Displays 5 registers starting from 1 with their index
	- ``f_inp 300`` Force logical state of input 300
	- ``uar /fb/lostreg.stp`` Save the value of register in the file ``lostreg.stp``

Oscilloscope
-------------


Graphic panel
-------------


Hardware configuration
----------------------


Important folders and files
---------------------------

Add new folder :ref:`fignewfolder`

.. _fignewfolder:
.. figure:: images/rde/newfolder.png
    :align: center
    :figwidth: 400px

    Add new folder to flash memory


rte-xxxx.bin

rte.cg

ipaddr.def

rhw.cfg

lostreg.stp

init.cfg

defalarm\_it.cfg


Registers
---------

:ref:`figgeneralstorage` show different types of registers and their allocation in memory.

.. _figgeneralstorage:
.. figure:: images/rde/general-storage.png
    :align: center
    :figwidth: 400px

    Register dimension

Bus configuration
-----------------


Axes configuration
------------------

Programming languages
=====================

R3
---


Predefined variables
--------------------

There are different predefined variables in R3. (put every vairable in its context)

``fr`` feed rate

``kff`` feed forward factor

``pro_gai``  position loop proportional gain

``epos`` position error when the position loops are closed with a predefined formula


Object block
------------

Object block is a C++ class, it is another option to write program in RDE. It is composed from a header file and a source file like like any ``C++ class``, in addition to these classic files, ``RDE`` use the ``obs file`` to describe the ``interface`` of the Object block.

In rte project, right click and add :ref:`ob-new`. A folder have to be selected for the compiled file. If the folder ob dosen't exist add it in the flash memory, see section files and folders.

.. _ob-new:
.. figure:: images/rde/ob-new.png
    :align: center
    :figwidth: 400px

    new Object block

    Create new Object block. right click in the tab program of an RTE project


.. _ob-new2:
.. figure:: images/rde/ob-new2.png
    :align: center
    :figwidth: 400px

    Write the OB name, select the folder of destination and check at least the first option


.. _ob-new3:
.. figure:: images/rde/ob-new3.png
    :align: center
    :figwidth: 400px

    Object block structure files


After the creation of a new object block we will obtain 4 files:
	- obs : object block interface file
	- h : C++ header
	- cpp : C++ source
	- obb : Object block binary file (compiled file)

Fig. :ref:`obobs`, :ref:`obheader` and :ref:`obcpp` show the auto generated files. As we can see the header and the source files have the structure of a classic C++ class with class name, class constructor and destructor.

.. _obobs:
.. figure:: images/rde/obobs.png
    :align: center
    :figwidth: 400px

    Obs

    Auto-generated OBS file


.. _obheader:
.. figure:: images/rde/obheader.png
    :align: center
    :figwidth: 400px

    Header

    Auto-generated C++ header


.. _obcpp:
.. figure:: images/rde/obcpp.png
    :align: center
    :figwidth: 400px

    Source

    Auto-generated C++ source


As any class of an object oriented language, an Object block have ``methods`` (functions) and ``fields`` (variables). Public methods and fields that can be accessed from an R3 program should be written in the obs file respectively in the methods and properties blocks.
Properties could be only of simple C++ types: BOOL, I8, I16, I32, U8, U16, U32, INT, FLOAT, REAL, CHAR,could not be of struct type.
The source file where the code is implemented is written in the block implementation.

.. _obsex:
.. figure:: images/rde/obs-example.png
    :align: center
    :figwidth: 400px

    Obs example file


As any object oreinted language, a class have to be instantiated before using it. In the configuration tab of an RTE project, right click Object block and add :ref:`obclass`. A class could have more than one instance. An ``OB`` is similar to an ``FB (Function block)`` in ``PLC`` programming.

.. _obclass:
.. figure:: images/rde/ob-class.png
    :align: center
    :figwidth: 400px

    OB Class or OB Instance

    Add a class than add an instance. In the figure we can see 2 classes : ``rc_mgv`` and ``rc_motorwheel``, and one instance of the first class and two instances of the second one


.. _obinstancepar:
.. figure:: images/rde/ob-instancepar.png
    :align: center
    :figwidth: 400px

    Object block instance parameters. In the column ``Value`` we can initialize the variables. To keep the program easy to read, it is better to initialize OB properties in R3. Note that properties declared as ``ro`` (read-only) are not shown here


Suppose we have the class ``rc\_mgv`` and its instance ``agv``, as in :ref:`obclass`. We can call in R3 the method ``get_status`` of the class ``rc_mgv`` as we call it in C++: ``agv.get_status(AgvStatus)``. We can access properties using also the dot operator for reading or writing: ``agv.DRIVING_MODE_TAPE = 4`` or ``if(agv.TAPE_FOLLOW_LEFT)``.

If we defined a structure in the obs file we can use it to define a variable of that type in R3 using the dot operator.


OB Predefined example
^^^^^^^^^^^^^^^^^^^^^

In menu file, workspace, specials, predefined examples, we can find the example OB: Use and OB implementation. This example provide the source code an OB, ``rc_belt``, that handle a belt and a rules and task 1 implementation.
The Class ``rc_belt`` is an OB that can be find in the Object Block library. The example use another OB from the standard library, ``rc_axis``, without providing its source code.

Refer to the official Object Block documentation for more informations about OB classes.

.. _obbeltexample:
.. figure:: images/rde/ob-belt-example.png
    :align: center
    :figwidth: 400px

    OB: Use and OB implementation predefined example


In the obs file of ``rc_belt``, we can see the interface of the Class, how to use another class by importing it, define inputs and outputs and some methods. Note that input and outputs deffer only with the keyword ``ro``. When an property is declared as read only behave like an output, otherwise behave like an input.

In the implementation we can see the call to two C++ source files. In this OB, 2 classes were defined. The class ``rc_belt``, that inherit from ``rc_belt_base``, and the class ``RCBelt``.

A detailed example about OB implementation will be provided in the chapter related to motion control.

RTE project
===========

Tasks
-----

Rules
-----

R3 example
----------

OB example
----------

Axis control example
=====================


Axis configuration
------------------

Power set and power handling
----------------------------

Velocity control
----------------

Position control
----------------
