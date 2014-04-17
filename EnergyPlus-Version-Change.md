> [Wiki](Home) ▸ **EnergyPlus Version Change**

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

In openstudiocore/ruby/openstudio/sketchup_plugin/lib/CommandManager.rb, update the IDF import failure message instructing the user to upgrade the idf to the latest version.

In openstudiocore/ruby/openstudio/sketchup_plugin/lib/PluginManager.rb, update the energyplus_version method to return the latest version.

In RunManager's BasementJob.cpp and SlabJob.cpp, update ToolVersion tv(foo,bar).

In openstudiocore/src/utilities/sql/SqlFile_Impl.cpp, update the _insert_ query to the use the latest version, and update the _select_ query to look for the latest version in addition to all previous versions.

In openstudiocore/src/openstudio_lib/RunTabView.cpp, update the locateEnergyPlus method to search for the latest version.

In top level CMakeLists.txt update ENERGYPLUS_VERSION.

Update IddFile_GTest.cpp version strings.

Update RunManagerHelpers.rb version strings.

Update TimeDependentValuation_Test.rb version strings.

Update ModelToRad.rb version strings.

Update DaylightSim_Test.rb version strings.

Update ModelToRad_Test.rb version strings.

Update AdvancedRubyWorkflow1_Test.rb version strings.

Update AdvancedRubyWorkflow3_Test.rb version strings.

Update ParallelEnergyPlus_Test.rb version strings.

Update RunManagerWatcher_Test.rb version strings.

Version translate openstudiocore/resources/runmanager/5ZoneWarmest.idf

Update #define ENERGYPLUS_VERSION "8.1" in ForwardTranslator.cpp
