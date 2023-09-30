        var csvData = [];
        var selectedCell = null;
        
        function loadCSV() {
            var fileInput = document.getElementById('csvFile');
            var file = fileInput.files[0];
            var reader = new FileReader();
            
            reader.onload = function(e) {
                var contents = e.target.result;
                csvData = parseCSV(contents);
                renderTable();
            };
            
            reader.readAsText(file);
        }
        
        function parseCSV(csv) {
            var lines = csv.split('\n');
            var data = [];
            
            for (var i = 0; i < lines.length; i++) {
                var cells = lines[i].split(',');
                data.push(cells);
            }
            return data;
        }
        
        function renderTable() {
            var table = document.getElementById('dataTable');
            table.innerHTML = '';
            
            for (var i = 0; i < csvData.length; i++) {
                var row = document.createElement('tr');
                
                for (var j = 0; j < csvData[i].length; j++) {
                    var cell = document.createElement(i === 0 ? 'th' : 'td');
                    cell.textContent = csvData[i][j];
                    
                    cell.setAttribute('contenteditable', 'true');
                    cell.classList.add('editable');
                    cell.addEventListener('input', function() {
                        var rowIndex = this.parentNode.rowIndex;
                        var cellIndex = this.cellIndex;
                        csvData[rowIndex][cellIndex] = this.textContent;
                    });
                    
                    row.appendChild(cell);
                }
                
                table.appendChild(row);
            }
        }
        
        function addRow() {
            var table = document.getElementById('dataTable');
            var rowCount = table.rows.length;
            var columnCount = csvData[0].length;
            var newRow = table.insertRow(rowCount);
            
            for (var i = 0; i < columnCount; i++) {
                var cell = newRow.insertCell(i);
                
                cell.setAttribute('contenteditable', 'true');
                cell.classList.add('editable');
                cell.addEventListener('input', function() {
                    var rowIndex = this.parentNode.rowIndex;
                    var cellIndex = this.cellIndex;
                    csvData[rowIndex][cellIndex] = this.textContent;
                });
            }
            
            csvData.push(new Array(columnCount).fill(''));
        }
        
        function addColumn() {
            var table = document.getElementById('dataTable');
            var rowCount = table.rows.length;
            var columnCount = csvData[0].length;
            
            if (selectedCell === null) {
                // No cell selected, add new column at last position
                for (var i = 0; i < rowCount; i++) {
                    var row = table.rows[i];
                    var cell = row.insertCell(columnCount);
                    
                    cell.setAttribute('contenteditable', 'true');
                    cell.classList.add('editable');
                    cell.addEventListener('input', function() {
                        var rowIndex = this.parentNode.rowIndex;
                        var cellIndex = this.cellIndex;
                        csvData[rowIndex][cellIndex] = this.textContent;
                    });
                    
                    csvData[i].push('');
                }
            } else {
                // Cell selected, add new column after selected cell
                var selectedRowIndex = selectedCell.parentNode.rowIndex;
                var selectedCellIndex = selectedCell.cellIndex;
                
                for (var i = 0; i < rowCount; i++) {
                    var row = table.rows[i];
                    var cell = row.insertCell(selectedCellIndex + 1);
                    
                    cell.setAttribute('contenteditable', 'true');
                    cell.classList.add('editable');
                    cell.addEventListener('input', function() {
                        var rowIndex = this.parentNode.rowIndex;
                        var cellIndex = this.cellIndex;
                        csvData[rowIndex][cellIndex] = this.textContent;
                    });
                    
                    csvData[i].splice(selectedCellIndex + 1, 0, '');
                }
            }
        }
        
        function createCSV() {
            var rowCount = parseInt(prompt('Enter the number of rows:'));
            var columnCount = parseInt(prompt('Enter the number of columns:'));
            
            if (!isNaN(rowCount) && !isNaN(columnCount) && rowCount > 0 && columnCount > 0) {
                csvData = new Array(rowCount);
                
                for (var i = 0; i < rowCount; i++) {
                    csvData[i] = new Array(columnCount).fill('');
                }
                
                renderTable();
            } else {
                alert('Invalid input! Please enter valid row and column counts.');
            }
        }
        
        function saveCSV() {
            var csvContent = '';
            
            for (var i = 0; i < csvData.length; i++) {
                csvContent += csvData[i].join(',') + '\n';
            }
            
            var csvBlob = new Blob([csvContent], { type: 'text/csv' });
            var link = document.createElement('a');
            link.href = URL.createObjectURL(csvBlob);
            link.download = 'modified.csv';
            link.click();
        }
        
        function selectCell(cell) {
            if (selectedCell !== null) {
                selectedCell.classList.remove('selected');
            }
            
            cell.classList.add('selected');
            selectedCell = cell;
        }
    
