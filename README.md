<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Transition Table and Diagram</title>
</head>
<style>
    body {
        font-family: 'Poppins', sans-serif;
        background: linear-gradient(135deg, #f0f8ff, #b3e5fc);
        color: #333;
        text-align: center;
        margin: 0;
        padding: 20px;
    }
    
    table {
        margin: 20px auto;
        border-collapse: collapse;
        width: 80%;
        box-shadow: 0px 4px 12px rgba(0, 0, 0, 0.2);
        border-radius: 8px;
        overflow: hidden;
    }
    
    table,
    th,
    td {
        border: 1px solid #ddd;
        padding: 12px;
    }
    
    th {
        background-color: #00796b;
        color: #ffffff;
        font-weight: bold;
    }
    
    td {
        background-color: #e0f2f1;
    }
    
    .diagram {
        margin-top: 30px;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: wrap;
    }
    
    .state {
        display: inline-block;
        width: 50px;
        height: 50px;
        line-height: 50px;
        border-radius: 50%;
        background: linear-gradient(145deg, #00796b, #004d40);
        color: #ffffff;
        font-weight: bold;
        position: relative;
        box-shadow: 0 6px 10px rgba(0, 0, 0, 0.2);
        transition: transform 0.3s, box-shadow 0.3s;
        fill: #004d40;
        stroke: #000000;
        stroke-width: 2px;
    }
    
    .state:hover {
        transform: scale(1.1);
        box-shadow: 0 8px 15px rgba(0, 0, 0, 0.3);
    }
    
    .arrow {
        font-size: 24px;
        display: flex;
        align-items: center;
        position: relative;
        margin: 0 15px;
        font-weight: bold;
        color: #004d40;
    }
    
    .arrow span {
        font-size: 24px;
    }
    
    .input-label {
        position: absolute;
        top: -25px;
        font-size: 12px;
        font-weight: bold;
        color: #004d40;
    }
    
    #error-message {
        color: #d32f2f;
        font-weight: bold;
        margin-top: 10px;
    }
    
    #reset-button {
        margin-top: 20px;
        padding: 12px 25px;
        font-size: 16px;
        background: linear-gradient(135deg, #ff5252, #e53935);
        color: white;
        border: none;
        cursor: pointer;
        border-radius: 5px;
        transition: background-color 0.3s, transform 0.3s;
    }
    
    #reset-button:hover {
        background: #004d40;
        transform: scale(1.05);
    }
    
    svg {
        max-width: 100%;
        height: auto;
    }
    
    .label {
        font-family: 'Poppins', sans-serif;
        font-size: 14px;
        fill: white;
        text-anchor: middle;
        alignment-baseline: middle;
    }
    /* Final State with Double Stroke */
    
    .outer-stroke {
        fill: none;
        stroke: #000000;
        stroke-width: 2px;
    }
    
    .final-state {
        fill: #004d40;
        stroke: #000000;
        stroke-width: 2px;
    }
    /* Mobile responsiveness */
    
    @media (max-width: 600px) {
        table {
            width: 90%;
        }
        .state {
            width: 40px;
            height: 40px;
            line-height: 40px;
            margin: 15px;
        }
        .arrow {
            font-size: 20px;
        }
        #reset-button {
            width: 150px;
            font-size: 14px;
        }
    }
</style>

<body>
    <h1>NFA Transition Table</h1>
    <table>
        <tr>
            <th>Current State</th>
            <th>Input 0</th>
            <th>Input 1</th>
        </tr>
        <tr>
            <td>A (Initial)</td>
            <td><input type="text" id="A-0" onchange="updateTransition('A', 0)" placeholder="Next State"></td>
            <td><input type="text" id="A-1" onchange="updateTransition('A', 1)" placeholder="Next State"></td>
        </tr>
        <tr>
            <td>B</td>
            <td><input type="text" id="B-0" onchange="updateTransition('B', 0)" placeholder="Next State"></td>
            <td><input type="text" id="B-1" onchange="updateTransition('B', 1)" placeholder="Next State"></td>
        </tr>
        <tr>
            <td>C</td>
            <td><input type="text" id="C-0" onchange="updateTransition('C', 0)" placeholder="Next State"></td>
            <td><input type="text" id="C-1" onchange="updateTransition('C', 1)" placeholder="Next State"></td>
        </tr>
        <tr>
            <td>D (Final)</td>
            <td><input type="text" id="D-0" onchange="updateTransition('D', 0)" placeholder="Next State"></td>
            <td><input type="text" id="D-1" onchange="updateTransition('D', 1)" placeholder="Next State"></td>
        </tr>
    </table>

    <h2>NFA Transition Diagram</h2>
    <div class="button-container">
        <button id="reset-button" onclick="resetTable()">Reset Table</button>
    </div>
    <div id="error-message"></div>
    <pre id="transition-display"></pre>

    <svg id="diagram" width="600" height="400">
        <defs>
            <marker id="arrowhead" markerWidth="10" markerHeight="3" refX="10" refY="3.5" orient="auto">
                <polygon points="0 0, 10 3.5, 0 7" fill="black" />
            </marker>
        </defs>

        <!-- States -->
        <circle cx="250" cy="100" r="30" class="state initial" />
        <text x="250" y="105" class="label">A</text>

        <circle cx="150" cy="250" r="30" class="state" />
        <text x="150" y="255" class="label">B</text>

        <circle cx="350" cy="250" r="30" class="state" />
        <text x="350" y="255" class="label">C</text>

       <!-- Final State D with Double Stroke Effect -->
<!-- Outer white stroke -->
<circle cx="500" cy="150" r="35" class="state outer-stroke" />
<!-- Inner black stroke with final styling -->
<circle cx="500" cy="150" r="30" class="state final-state" />
<text x="500" y="155" class="label">D</text>

        <!-- Arrows (Transitions) -->
        <line x1="250" y1="130" x2="150" y2="220" class="arrow" marker-end="url(#arrowhead)" />
        <line x1="250" y1="130" x2="350" y2="220" class="arrow" marker-end="url(#arrowhead)" />
        <line x1="350" y1="220" x2="500" y2="150" class="arrow" marker-end="url(#arrowhead)" />
        <line x1="150" y1="220" x2="500" y2="150" class="arrow" marker-end="url(#arrowhead)" />

        <!-- Transition Labels -->
        <text x="200" y="170" class="label">0</text>
        <text x="300" y="170" class="label">1</text>
        <text x="400" y="190" class="label">0, 1</text>
    </svg>
    <script>
        // Updated transitions object to include state D
        const transitions = {
            'A': {
                '0': null,
                '1': null
            },
            'B': {
                '0': null,
                '1': null
            },
            'C': {
                '0': null,
                '1': null
            },
            'D': {
                '0': null,
                '1': null
            } // New state D
        };

        function updateTransition(state, input) {
            const errorMessage = document.getElementById("error-message");
            const nextState = document.getElementById(`${state}-${input}`).value.toUpperCase();

            // Allow state D in addition to A, B, and C
            if (['A', 'B', 'C', 'D'].includes(nextState)) {
                transitions[state][input] = nextState;
                errorMessage.textContent = '';
            } else {
                errorMessage.textContent = `Invalid state: "${nextState}". Please enter A, B, C, or D.`;
                return;
            }

            console.log(transitions); // Log the transitions object
            buildDiagram(); // Build the diagram after updating transitions
        }

        function buildDiagram() {
            const diagramContainer = document.getElementById("diagram");
            diagramContainer.innerHTML = ''; // Clear previous diagram

            // Create SVG for the diagram
            const svg = document.createElementNS("http://www.w3.org/2000/svg", "svg");
            svg.setAttribute("width", "600");
            svg.setAttribute("height", "400");
            svg.setAttribute("viewBox", "0 0 600 400");

            // Define state positions in a layout including state D
            const positions = {
                'A': {
                    x: 250,
                    y: 100
                }, // Top center for state A
                'B': {
                    x: 150,
                    y: 300
                }, // Bottom left for state B
                'C': {
                    x: 350,
                    y: 300
                }, // Bottom right for state C
                'D': {
                    x: 500,
                    y: 150
                } // Right side for state D (final)
            };

            // Draw states as circles with labels
            for (const state in transitions) {
                const pos = positions[state];
                const circle = document.createElementNS("http://www.w3.org/2000/svg", "circle");
                circle.setAttribute("cx", pos.x);
                circle.setAttribute("cy", pos.y);
                circle.setAttribute("r", "30");
                circle.setAttribute("class", `state ${state === 'A' ? 'initial' : ''} ${state === 'D' ? 'final' : ''}`); // Class for styling initial/final states

                // Add label inside the circle
                const text = document.createElementNS("http://www.w3.org/2000/svg", "text");
                text.setAttribute("x", pos.x);
                text.setAttribute("y", pos.y + 5); // Center text vertically
                text.setAttribute("class", "label"); // Apply label class for styles
                text.textContent = state; // Set the state label (A, B, C, or D)

                svg.appendChild(circle);
                svg.appendChild(text);
            }

            // Draw arrows based on transitions
            for (const state in transitions) {
                for (const input in transitions[state]) {
                    const nextState = transitions[state][input];
                    if (nextState) {
                        const startPos = positions[state];

                        if (nextState === state) {
                            // Draw a looping arrow above the circle
                            const path = document.createElementNS("http://www.w3.org/2000/svg", "path");
                            const radius = 30; // Circle radius
                            const loopRadius = 20; // Loop radius (adjust for spacing)
                            const loopOffsetY = 40; // Vertical offset to position loop above the circle

                            // Create a path for the loop
                            const loopPath = `M${startPos.x - radius},${startPos.y - loopOffsetY} 
                                              A${loopRadius},${loopRadius} 0 0,1 ${startPos.x + radius},${startPos.y - loopOffsetY}`;
                            path.setAttribute("d", loopPath);
                            path.setAttribute("stroke", "black");
                            path.setAttribute("fill", "none");
                            path.setAttribute("marker-end", "url(#arrowhead)");
                            svg.appendChild(path);

                            // Add input label on the loop above
                            const label = document.createElementNS("http://www.w3.org/2000/svg", "text");
                            label.setAttribute("x", startPos.x - 5); // Center the label above the loop
                            label.setAttribute("y", startPos.y - loopOffsetY - 10); // Position label above the loop
                            label.setAttribute("class", "input-label");
                            label.textContent = input; // Set the input label (0 or 1)
                            svg.appendChild(label);

                        } else {
                            // Draw the arrow line for different states
                            const endPos = positions[nextState];
                            const line = document.createElementNS("http://www.w3.org/2000/svg", "line");
                            line.setAttribute("x1", startPos.x);
                            line.setAttribute("y1", startPos.y + 30); // Position the line below the circle
                            line.setAttribute("x2", endPos.x);
                            line.setAttribute("y2", endPos.y - 30); // Position the line above the circle
                            line.setAttribute("stroke", "black"); // Set the stroke color
                            line.setAttribute("stroke-width", "2"); // Set the stroke width
                            line.setAttribute("marker-end", "url(#arrowhead)"); // Add arrowhead

                            // Add input label on the line
                            const label = document.createElementNS("http://www.w3.org/2000/svg", "text");
                            const midX = (startPos.x + endPos.x) / 2;
                            const midY = (startPos.y + endPos.y) / 2;
                            label.setAttribute("x", midX);
                            label.setAttribute("y", midY - 10); // Position label above the line
                            label.setAttribute("class", "input-label");
                            label.textContent = input; // Set the input label (0 or 1)

                            svg.appendChild(line);
                            svg.appendChild(label);
                        }
                    }
                }
            }

            // Define arrowhead marker
            const defs = document.createElementNS("http://www.w3.org/2000/svg", "defs");
            const marker = document.createElementNS("http://www.w3.org/2000/svg", "marker");
            marker.setAttribute("id", "arrowhead");
            marker.setAttribute("markerWidth", "10");
            marker.setAttribute("markerHeight", "7");
            marker.setAttribute("refX", "5");
            marker.setAttribute("refY", "3.5");
            marker.setAttribute("orient", "auto");

            const arrowPath = document.createElementNS("http://www.w3.org/2000/svg", "path");
            arrowPath.setAttribute("d", "M0,0 L0,7 L10,3.5 Z");
            arrowPath.setAttribute("fill", "black"); // Arrowhead color

            marker.appendChild(arrowPath);
            defs.appendChild(marker);
            svg.appendChild(defs);

            // Append the SVG to the diagram container
            diagramContainer.appendChild(svg);
        }

        function resetTable() {
            for (const state in transitions) {
                transitions[state]['0'] = null;
                transitions[state]['1'] = null;
            }

            document.getElementById("A-0").value = '';
            document.getElementById("A-1").value = '';
            document.getElementById("B-0").value = '';
            document.getElementById("B-1").value = '';
            document.getElementById("C-0").value = '';
            document.getElementById("C-1").value = '';
            document.getElementById("D-0").value = ''; // Reset D
            document.getElementById("D-1").value = ''; // Reset D

            document.getElementById("diagram").innerHTML = '';
            document.getElementById("error-message").textContent = '';
        }
        for (const state in transitions) {
            const pos = positions[state];
            const circle = document.createElementNS("http://www.w3.org/2000/svg", "circle");
            circle.setAttribute("cx", pos.x);
            circle.setAttribute("cy", pos.y);
            circle.setAttribute("r", "30");

            // Apply the final-state class if it's the final state (e.g., 'D')
            if (state === 'D') {
                circle.classList.add("state", "final-state"); // Add both 'state' and 'final-state' classes
            } else {
                circle.classList.add("state"); // Only 'state' class for other states
            }

            svg.appendChild(circle);
        }
    </script>


</body>

</html>

