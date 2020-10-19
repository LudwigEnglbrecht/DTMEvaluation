# To run the simulation run the following commands:

# The following command executes a business process 8.000 times.
# All process are stored in ./process_instances/ and sorted by process instance

python3 simulate_document_flow_python3_prototyp.py


# To generate a structure of all files belonging to one phase run the following command.
# After the execution all previously generated files are sorted by phase.
# This is useful for having a phase-wise representation of the generated files.

mkdir ./process_instances_sorted_by_phase/

mkdir ./process_instances_sorted_by_phase/phase_00/
for f in  ./process_instances/*/*offer_00*.xml; do     
cp "$f"    "./process_instances_sorted_by_phase/phase_00/${f##*/}"   
done


mkdir ./process_instances_sorted_by_phase/phase_01/
for f in  ./process_instances/*/*offer_01*.xml; do     
cp "$f"    "./process_instances_sorted_by_phase/phase_01/${f##*/}"   
done


mkdir ./process_instances_sorted_by_phase/phase_02/
for f in  ./process_instances/*/*offer_02*.xml; do     
cp "$f"    "./process_instances_sorted_by_phase/phase_02/${f##*/}"   
done


mkdir ./process_instances_sorted_by_phase/phase_03/
for f in  ./process_instances/*/*offer_03*.xml; do     
cp "$f"    "./process_instances_sorted_by_phase/phase_03/${f##*/}"   
done