
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tutor de Programación - DeepSeek</title>
    <style>
        :root {
            --primary: #2563eb;
            --secondary: #64748b;
            --success: #22c55e;
            --warning: #eab308;
            --danger: #ef4444;
            --light: #f8fafc;
            --dark: #1e293b;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            overflow: hidden;
        }
        
        header {
            background: var(--primary);
            color: white;
            padding: 20px;
            text-align: center;
        }
        
        .header-content {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
        }
        
        .logo {
            font-size: 2rem;
            font-weight: bold;
        }
        
        .main-content {
            display: grid;
            grid-template-columns: 300px 1fr;
            min-height: 600px;
        }
        
        .sidebar {
            background: var(--light);
            padding: 20px;
            border-right: 1px solid #e2e8f0;
        }
        
        .language-selector {
            margin-bottom: 30px;
        }
        
        select, button {
            width: 100%;
            padding: 12px;
            margin: 8px 0;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
        }
        
        button {
            background: var(--primary);
            color: white;
            border: none;
            cursor: pointer;
            transition: background 0.3s;
        }
        
        button:hover {
            background: #1d4ed8;
        }
        
        button:disabled {
            background: var(--secondary);
            cursor: not-allowed;
        }
        
        .lessons-list {
            max-height: 400px;
            overflow-y: auto;
        }
        
        .lesson-item {
            padding: 12px;
            margin: 8px 0;
            background: white;
            border: 1px solid #e2e8f0;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .lesson-item:hover {
            background: #eff6ff;
            border-color: var(--primary);
        }
        
        .lesson-item.active {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
        }
        
        .content-area {
            padding: 20px;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        
        .lesson-content {
            background: white;
            border: 1px solid #e2e8f0;
            border-radius: 8px;
            padding: 20px;
            flex: 1;
            overflow-y: auto;
            max-height: 300px;
        }
        
        .code-editor {
            flex: 1;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        
        .editor-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        textarea {
            width: 100%;
            height: 200px;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-family: 'Monaco', 'Menlo', 'Ubuntu Mono', monospace;
            font-size: 14px;
            resize: vertical;
        }
        
        .navigation {
            display: flex;
            gap: 10px;
            justify-content: space-between;
        }
        
        .feedback {
            padding: 15px;
            border-radius: 8px;
            margin-top: 15px;
            display: none;
        }
        
        .feedback.success {
            background: #dcfce7;
            border: 1px solid #22c55e;
            color: #166534;
            display: block;
        }
        
        .feedback.error {
            background: #fee2e2;
            border: 1px solid #ef4444;
            color: #991b1b;
            display: block;
        }
        
        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            
            .sidebar {
                border-right: none;
                border-bottom: 1px solid #e2e8f0;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="header-content">
                <div class="logo">🧠</div>
                <h1>Tutor de Programación DeepSeek</h1>
            </div>
        </header>
        
        <div class="main-content">
            <div class="sidebar">
                <div class="language-selector">
                    <label for="language">Selecciona un lenguaje:</label>
                    <select id="language">
                        <option value="python">Python</option>
                        <option value="javascript">JavaScript</option>
                        <option value="java">Java</option>
                        <option value="cpp">C++</option>
                    </select>
                </div>
                
                <h3>Lecciones</h3>
                <div class="lessons-list" id="lessonsList">
                    <!-- Las lecciones se cargarán dinámicamente -->
                </div>
            </div>
            
            <div class="content-area">
                <div class="lesson-content" id="lessonContent">
                    <h2 id="lessonTitle">Bienvenido al Tutor de Programación</h2>
                    <p id="lessonText">Selecciona un lenguaje y una lección para comenzar.</p>
                </div>
                
                <div class="code-editor">
                    <div class="editor-header">
                        <h3>Práctica - Escribe tu código:</h3>
                        <button onclick="runCode()" style="width: auto;">▶ Ejecutar</button>
                    </div>
                    <textarea id="codeEditor" placeholder="Escribe tu código aquí..."></textarea>
                    <button onclick="checkSolution()">Verificar mi solución</button>
                    
                    <div id="feedback" class="feedback"></div>
                </div>
                
                <div class="navigation">
                    <button id="prevBtn" onclick="prevLesson()" disabled>← Lección anterior</button>
                    <button id="nextBtn" onclick="nextLesson()">Siguiente lección →</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Base de datos de lecciones
        const lessons = {
            python: [
                {
                    title: "Introducción a Python",
                    content: `Python es un lenguaje de programación interpretado, de alto nivel y con una sintaxis clara y legible.

Características principales:
- Fácil de aprender y usar
- Lenguaje interpretado (no necesita compilación)
- Tipado dinámico
- Multiparadigma

¡Empecemos con lo básico!

La función print() se utiliza para mostrar mensajes:
>>> print("Hola, mundo!")
Hola, mundo!

Las variables se crean simplemente asignando un valor:
>>> mensaje = "Bienvenido a Python"
>>> print(mensaje)
Bienvenido a Python`,
                    template: '# Escribe tu código aquí\nprint("Hola, mundo!")',
                    validate: (code) => {
                        return code.includes('print(') ? 
                            {success: true, message: "¡Excelente! Has usado print() correctamente."} :
                            {success: false, message: "Intenta usar la función print() para mostrar un mensaje."};
                    }
                },
                {
                    title: "Variables y Tipos de Datos",
                    content: `En Python, tenemos varios tipos de datos básicos:

- Enteros (int): números sin decimales (ej: 5, -3, 1000)
- Flotantes (float): números con decimales (ej: 3.14, -0.5, 2.0)
- Cadenas (str): texto entre comillas (ej: "Hola", 'Python')
- Booleanos (bool): True o False

Puedes verificar el tipo de una variable con la función type().

Ejemplos:
>>> edad = 25
>>> type(edad)
<class 'int'>

>>> precio = 19.99
>>> type(precio)
<class 'float'>`,
                    template: '# Crea variables de diferentes tipos\nnombre = "Ana"\nedad = 25\naltura = 1.65\nes_estudiante = True',
                    validate: (code) => {
                        const lines = code.split('\n').filter(line => !line.trim().startsWith('#') && line.trim() !== '');
                        return lines.length >= 2 ? 
                            {success: true, message: "¡Bien hecho! Has creado variables correctamente."} :
                            {success: false, message: "Intenta crear al menos dos variables diferentes."};
                    }
                }
            ],
            javascript: [
                {
                    title: "Introducción a JavaScript",
                    content: `JavaScript es el lenguaje de programación de la web. Se ejecuta en los navegadores y permite crear páginas web interactivas.

Características principales:
- Interpretado por los navegadores
- Orientado a objetos
- Tipado dinámico
- Funciones como ciudadanos de primera clase

Para mostrar mensajes en la consola:
console.log("Hola, mundo!");

Las variables se pueden declarar con let, const o var:
let mensaje = "Bienvenido a JavaScript";
console.log(mensaje);`,
                    template: '// Escribe tu código aquí\nconsole.log("Hola, mundo!");',
                    validate: (code) => {
                        return code.includes('console.log(') ? 
                            {success: true, message: "¡Perfecto! Has usado console.log() correctamente."} :
                            {success: false, message: "Intenta usar console.log() para mostrar un mensaje."};
                    }
                }
            ],
            java: [
                {
                    title: "Introducción a Java",
                    content: `Java es un lenguaje de programación orientado a objetos, compilado y fuertemente tipado.

Características principales:
- "Escribe una vez, ejecuta en cualquier lugar"
- Fuertemente tipado
- Orientación a objetos
- Gran ecosistema de librerías

La estructura básica de un programa Java:

public class HolaMundo {
    public static void main(String[] args) {
        System.out.println("Hola, mundo!");
    }
}

Las variables deben declararse con su tipo:
String mensaje = "Bienvenido a Java";
int numero = 10;`,
                    template: 'public class Main {\n    public static void main(String[] args) {\n        // Escribe tu código aquí\n    }\n}',
                    validate: (code) => {
                        return code.includes('System.out.println(') ? 
                            {success: true, message: "¡Excelente! Has usado System.out.println() correctamente."} :
                            {success: false, message: "Intenta usar System.out.println() para mostrar un mensaje."};
                    }
                }
            ],
            cpp: [
                {
                    title: "Introducción a C++",
                    content: `C++ es un lenguaje de programación compilado, de propósito general y con soporte para programación orientada a objetos.

Características principales:
- Alto rendimiento
- Compilado a código nativo
- Soporte para programación orientada a objetos
- Mayor control sobre el hardware

La estructura básica de un programa C++:

#include <iostream>

int main() {
    std::cout << "Hola, mundo!" << std::endl;
    return 0;
}

Las variables deben declararse con su tipo:
std::string mensaje = "Bienvenido a C++";
int numero = 10;`,
                    template: '#include <iostream>\n\nint main() {\n    // Escribe tu código aquí\n    return 0;\n}',
                    validate: (code) => {
                        return code.includes('std::cout') ? 
                            {success: true, message: "¡Bien hecho! Has usado std::cout correctamente."} :
                            {success: false, message: "Intenta usar std::cout para mostrar un mensaje."};
                    }
                }
            ]
        };

        // Estado de la aplicación
        let currentLanguage = 'python';
        let currentLesson = 0;

        // Inicializar la aplicación
        function initApp() {
            loadLessonsList();
            document.getElementById('language').addEventListener('change', (e) => {
                currentLanguage = e.target.value;
                currentLesson = 0;
                loadLessonsList();
                loadLesson();
            });
            loadLesson();
        }

        // Cargar la lista de lecciones
        function loadLessonsList() {
            const lessonsList = document.getElementById('lessonsList');
            lessonsList.innerHTML = '';
            
            lessons[currentLanguage].forEach((lesson, index) => {
                const lessonItem = document.createElement('div');
                lessonItem.className = `lesson-item ${index === currentLesson ? 'active' : ''}`;
                lessonItem.innerHTML = `Lección ${index + 1}: ${lesson.title}`;
                lessonItem.onclick = () => {
                    currentLesson = index;
                    loadLesson();
                    loadLessonsList();
                };
                lessonsList.appendChild(lessonItem);
            });
        }

        // Cargar la lección actual
        function loadLesson() {
            const lesson = lessons[currentLanguage][currentLesson];
            document.getElementById('lessonTitle').textContent = lesson.title;
            document.getElementById('lessonText').textContent = lesson.content;
            document.getElementById('codeEditor').value = lesson.template;
            
            // Actualizar botones de navegación
            document.getElementById('prevBtn').disabled = currentLesson === 0;
            document.getElementById('nextBtn').disabled = currentLesson === lessons[currentLanguage].length - 1;
            
            // Ocultar feedback
            document.getElementById('feedback').className = 'feedback';
        }

        // Navegar a la lección anterior
        function prevLesson() {
            if (currentLesson > 0) {
                currentLesson--;
                loadLesson();
                loadLessonsList();
            }
        }

        // Navegar a la siguiente lección
        function nextLesson() {
            if (currentLesson < lessons[currentLanguage].length - 1) {
                currentLesson++;
                loadLesson();
                loadLessonsList();
            }
        }

        // Verificar la solución
        function checkSolution() {
            const code = document.getElementById('codeEditor').value;
            const validation = lessons[currentLanguage][currentLesson].validate(code);
            
            const feedback = document.getElementById('feedback');
            feedback.textContent = validation.message;
            feedback.className = `feedback ${validation.success ? 'success' : 'error'}`;
        }

        // Ejecutar el código (simulación)
        function runCode() {
            const code = document.getElementById('codeEditor').value;
            alert("Ejecutando código:\n\n" + code + "\n\n(En una implementación real, esto ejecutaría el código en un entorno seguro)");
        }

        // Iniciar la aplicación cuando se cargue la página
        window.onload = initApp;
    </script>
</body>
</html>
