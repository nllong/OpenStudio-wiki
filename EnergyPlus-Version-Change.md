EnergyPlus Migration

Procedure:

Create new ProposedEnergy+.idd.  I do this by diffing previous version idd and new version idd and copying over changes.

Analyze diffs in idd versions and adjust the energyplus translator as needed to write valid idf files in the new version.  Changes may also be made to the OpenStudio Model classes but they must not break the existing api.

Rename file openstudiocore/resources/energyplus/Energy+.idd to openstudiocore/resources/energyplus/VX-Y-Z-Energy+.idd.  This is an archive of the previous version idd file in its unmodified form.

Copy new Energy+.idd from EnergyPlus installation to openstudiocore/resources/energyplus/Energy+.idd

Version translate idf files located in openstudiocore/resources/ using the EnergyPlus version translator.

Update openstudiocore/ruby/openstudio/energyplus/find_energyplus.rb build_version method.

Update various example files in openstudiocore/ruby/openstudio/examples which use find_energyplus.

Update various test files in openstudiocore/ruby/openstudio/examples/test which use find_energyplus.

Update ENERGYPLUS_VERSION in openstudiocore/CMakeLists.txt

Run unit tests and fix things that are broken. 

Run regression tests in openstudio-resources, especially model simulation tests.

In EnergyPlusJob.cpp, update EnergyPlusJob::getToolVersionImpl line ToolVersion tv(foo,bar) where foo and bar are the major and minor versions.
