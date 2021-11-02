pragma solidity  ^0.8.9;

contract TareaContract {
     uint nextId;
     
     struct Tarea {
         uint id;
         string name;
         string description;
     }
     
     Tarea[] Tareas;  
  
    function createTarea (string memory _name, string memory _description) public {
        Tareas.push(Tarea(nextId, _name, _description));
        nextId++;
     }
     
     
    function findIndex(uint _id) internal view returns (uint) {
        for (uint i = 0; i < Tareas.length; i++) {
             if (Tareas[i].id == _id) {
                    return i;
             }
        }
        revert('Tarea no encontrada');
    }
        
     function readTareas(uint _id) public view returns (uint, string memory, string memory) {
         uint index = findIndex(_id);
         return (Tareas[index].id, Tareas[index].name, Tareas[index].description);
    }
    
    function updateTarea(uint _id, string memory _name, string memory _description) public{
        uint index = findIndex(_id);
        Tareas[index].name= _name;
        Tareas[index].description = _description;
    }
    
    function deleteTareas(uint _id) public {
        uint index = findIndex(_id);
        delete Tareas[index];
    }
}
