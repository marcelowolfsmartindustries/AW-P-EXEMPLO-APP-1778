# Conteúdo

## Âmbito
- Criação de uma app para gerir escolas, cursos e alunos.
- Para este projecto 

## TECH STACK
- React c/ VITE

https://vitejs.dev/

- Bootstrap

https://getbootstrap.com/

- AXIOS

https://axios-http.com/docs/intro

## Aula 1 - Setup de instalação

https://vitejs.dev/guide/

- Abrir terminal e executar:
    ```bash
    npm create vite@latest app -- --template react
    ```

- Navegar para a pasta do projeto
    ```bash
    cd app
    ```

- Instalar os packages:
    ```bash
    npm i 
    ```

- Instalar o react-router-dom:
    ```bash
    npm i react-router-dom 
    ```

- Instalar o react-validation:
    ```bash
    npm i react-validation
    ```

- Instalar o validator:
    ```bash
    npm i validator
    ```

- Instalar o bootstrap:
    ```bash
    npm i bootstrap
    ```

- Instar o axios
    ```bash
    npm i axios
    ```

- Testar:
    ```bash
    npm run dev
    ➜  Local:   http://localhost:5174/
    ```

## Aula 2 - Estrutura do projeto e navegação entre páginas

- Antes de começar definir a seguinte estrutura:

    ```
    📦AW-P-EXEMPLO-APP-1778
    ┣ 📂app
    ┃ ┣ 📂public
    ┃ ┃ ┣ 📜logo-estg.svg (+)
    ┃ ┣ 📂src
    ┃ ┃ ┣ 📂assets
    ┃ ┃ ┣ 📂components (+)
    ┃ ┃ ┃ ┣ 📂public (+) 
    ┃ ┃ ┃ ┣ 📂secure (+)
    ┃ ┃ ┃ ┗ 📂shared (+)
    ┃ ┃ ┣ 📂services (+)
    ┃ ┃ ┣ 📂utils (+)
    ┃ ┃ ┣ 📜App.css
    ┃ ┃ ┣ 📜App.jsx
    ┃ ┃ ┣ 📜index.css
    ┃ ┃ ┗ 📜main.jsx
    ┃ ┣ 📜.eslintrc.cjs
    ┃ ┣ 📜.gitignore
    ┃ ┣ 📜index.html
    ┃ ┣ 📜package-lock.json
    ┃ ┣ 📜package.json
    ┃ ┣ 📜README.md
    ┃ ┣ 📜setupProxy.js
    ┃ ┗ 📜vite.config.js
    ┗ 📜README.md
    ```

- Criar os componentes shared (componentes partilhados por toda a app)

    ### Footer.jsx
    ```jsx
    import React from "react";

    const Footer = () => {
        return (
            <footer className="p-3 bg-dark text-white mt-4 fixed-bottom">
                <article>IPVC ESTG - Desevolvimento Web e Multimédia &copy; - 2023-2024</article>
            </footer>
        );
    };

    export default Footer;
    ```

    ### Header.jsx
    ```jsx
    import React from "react";

    const Header = () => {
        return (
            <header className="pb-3 mb-4 border-bottom">
            <a href="/" className="d-flex align-items-center text-dark text-decoration-none">
                <img src="/logo-estg.svg" alt="ESTG" className="mw-100" />
            </a>
            </header>
        );
    };

    export default Header;
    ```

- Criar os componentes public (componentes acedidos sem ser necessário autenticação)


    ### Home.jsx
    ```jsx
    import React from "react";
    import { Link } from "react-router-dom";

    const Home = () => {
    return (
        <main>
        <div className="container py-4">
            <div className="p-5 mb-4 bg-body-tertiary rounded">
            <div className="container-fluid py-5 ">
                <h1 className="display-5 fw-bold">Olá👋</h1>
                <div className="d-flex justify-content">
                <Link to={"/login"} className="btn btn-info btn-lg px-4">
                    Entrar
                </Link>
                <Link to={"/register"} className="btn btn-success btn-lg px-4 mx-2">
                    Registar
                </Link>
                </div>
            </div>
            </div>
        </div>
        </main>
    );
    };

    export default Home;
    ```

    ### Login.jsx

    ```jsx
    import React, {  } from "react";
    import { Link } from "react-router-dom";

    const Login = () => {
    return (
        <main>
        <div className="container py-4">
            <div className="p-5 mb-4 bg-body-tertiary rounded">
            <div className="container-fluid py-5 ">
                <h1 className="display-5 fw-bold">Login</h1>
                <div className="d-flex justify-content">
                <Link to={"/home"} className="btn btn-info btn-lg px-4">
                    Home
                </Link>
                <Link to={"/register"} className="btn btn-success btn-lg px-4 mx-2">
                    Registar
                </Link>
                </div>
            </div>
            </div>
        </div>
        </main>
    );
    };

    export default Login;

    ```

    ### Register.jsx
    ```jsx
    import React, {  } from "react";
    import { Link } from "react-router-dom";

    const Register = () => {
    return (
        <main>
        <div className="container py-4">
            <div className="p-5 mb-4 bg-body-tertiary rounded">
            <div className="container-fluid py-5 ">
                <h1 className="display-5 fw-bold">Registar</h1>
                <div className="d-flex justify-content">
                <Link to={"/home"} className="btn btn-info btn-lg px-4">
                    Home
                </Link>
                <Link to={"/login"} className="btn btn-success btn-lg px-4 mx-2">
                    Entrar 
                </Link>
                </div>
            </div>
            </div>
        </div>
        </main>
    );
    };

    export default Register;
    ```

- Alterar o App.js

    ```jsx
    import React, { } from "react";
    import { Route, Routes, Navigate } from "react-router-dom";
    import "bootstrap/dist/css/bootstrap.min.css";
    import "./App.css";

    //PUBLIC ROUTES
    import Home from "./components/public/Home";
    import Login from "./components/public/Login";
    import Register from "./components/public/Register";

    import Footer from "./components/shared/Footer";
    import Header from "./components/shared/Header";

    const App = () => {
    return (
        <div>
        <div className="container mt-3">
            <Header />
            <Routes>
            <Route exact path={"/"} element={<Home />} />
            <Route exact path="/login" element={<Login />} />
            <Route exact path="/register" element={<Register />} />
            <Route path="*" element={<Navigate to="/" />} />
            </Routes>
            <Footer />
        </div>
        </div>
    );
    };

    export default App;

    ```

- Alterar o main.jsx

    ```jsx
    import React from "react";
    import ReactDOM from "react-dom/client";
    import { BrowserRouter as Router } from 'react-router-dom'
    import "./index.css";
    import App from "./App";

    const root = ReactDOM.createRoot(document.getElementById("root"));
    root.render(
    <React.Fragment>
        <Router>
        <App />
        </Router>
    </React.Fragment>,
    );
    ```

- **Apagar todo o conteúdo em App.css e index.css**

- Testar:

    ```bash
    npm run dev
    ➜  Local:   http://localhost:5174/
    ```

## Aula 3 - Autenticação e autorização

- Criar os componentes de validação das rotas (src/utils)


    ### privateRoute.jsx
    ```jsx
    import { Outlet, Navigate } from 'react-router-dom'

    function PrivateRoutes() {
        const token = localStorage.getItem('token');
        
        if(token) {
            return <Outlet />
        }

        return <Navigate to='/' />
    }

    export default PrivateRoutes
    ```

    ### publicRoute.jsx
    ```jsx
    import { Outlet, Navigate } from 'react-router-dom'

    function PublicRoutes() {
        const token = localStorage.getItem('token');

        if(token) {
            return <Navigate to='/dashboard' />
        }
        return <Outlet />
    }

    export default PublicRoutes
    ```

- Criar o serviço de autentição (src/services/auth.service.js)

    ### auth.service.js
    ```javascript
    import axios from "axios";

    const API_URL = "https://aw-p-exemplo-1778.vercel.app/api/v2/auth/"; //URL DA VOSSA WEBI API!

    const register = (name, email, password) => {
    return axios.post(API_URL + "signup", {
        name,
        email,
        password,
        isAdmin: false
    }).then((response) => {
        if (response.data.name) {
        localStorage.setItem("name", response.data.name);
        localStorage.setItem("token", response.data.token);
        }

        return response.data;
    });
    };

    const login = (email, password) => {
    return axios.post(API_URL + "signin", { email, password, })
        .then((response) => {
        if (response.data.name) {
            localStorage.setItem("name", response.data.name);
            localStorage.setItem("token", response.data.token);
        }

        return response.data;
        });
    };

    const logout = () => {
    localStorage.clear();
    };

    const getCurrentUser = () => {
    return localStorage.getItem("name");
    };

    const AuthService = {
    register,
    login,
    logout,
    getCurrentUser,
    }

    export default AuthService;
    ```

- Alterar ficheiros de Login e Register

    ### Login.jsx

    ```jsx
    import React, { useState, useRef } from "react";
    import { Link, useNavigate } from "react-router-dom";
    import Form from "react-validation/build/form";
    import Input from "react-validation/build/input";
    import CheckButton from "react-validation/build/button";
    import AuthService from "../../services/auth.service";

    const required = (value) => {
    if (!value) {
        return (
        <div className="invalid-feedback d-block">
            É obrigatório!
        </div>
        );
    }
    };

    const Login = () => {
    const form = useRef();
    const checkBtn = useRef();

    const [username, setUsername] = useState("");
    const [password, setPassword] = useState("");
    const [loading, setLoading] = useState(false);
    const [message, setMessage] = useState("");

    const navigate = useNavigate();

    const onChangeUsername = (e) => {
        const username = e.target.value;
        setUsername(username);
    };

    const onChangePassword = (e) => {
        const password = e.target.value;
        setPassword(password);
    };

    const handleLogin = (e) => {
        e.preventDefault();

        setMessage("");
        setLoading(true);

        form.current.validateAll();

        if (checkBtn.current.context._errors.length === 0) {
        AuthService.login(username, password).then(
            () => {
            navigate("/dashboard");
            },
            (error) => {
            setLoading(false);
            setMessage("Credenciais erradas!");
            }
        );
        } else {
        setLoading(false);
        }
    };

    return (
        <main>
        <section>
            <div className="p-5 mb-4 bg-body-tertiary rounded-3">
            <div className="container-fluid py-5">

                <Form onSubmit={handleLogin} ref={form} className="col-4">
                <h1 className="h3 mb-3 fw-normal">Entrar</h1>
                <div className="form-group">
                    <label htmlFor="username">E-mail</label>
                    <Input
                    type="text"
                    className="form-control"
                    name="username"
                    value={username}
                    onChange={onChangeUsername}
                    validations={[required]}
                    />
                </div>

                <div className="form-group">
                    <label htmlFor="password">Password</label>
                    <Input
                    type="password"
                    className="form-control"
                    name="password"
                    value={password}
                    onChange={onChangePassword}
                    validations={[required]}
                    />
                </div>

                <div className="form-group">
                    <button className="btn btn-info mt-2" disabled={loading}>
                    {loading && (
                        <span className="spinner-border spinner-border-sm"></span>
                    )}
                    <span>Login</span>
                    </button>

                    <Link to={"/"} className="btn btn-secondary mt-2 mx-2">
                    Voltar
                    </Link>
                </div>

                {message && (
                    <div className="form-group mt-2">
                    <div className="alert alert-danger" role="alert">
                        {message}
                    </div>
                    </div>
                )}
                <CheckButton style={{ display: "none" }} ref={checkBtn} />
                </Form>
            </div>
            </div>
        </section>
        </main>
    );
    };

    export default Login;
    ```

    ### Register.jsx

    ```jsx
    import React, { useState, useRef } from "react";
    import Form from "react-validation/build/form";
    import Input from "react-validation/build/input";
    import CheckButton from "react-validation/build/button";
    import { isEmail } from "validator";
    import { Link, useNavigate } from "react-router-dom";

    import AuthService from "../../services/auth.service";

    const required = (value) => {
    if (!value) {
        return (
        <div className="invalid-feedback d-block">
            É obrigatório!
        </div>
        );
    }
    };

    const validEmail = (value) => {
    if (!isEmail(value)) {
        return (
        <div className="invalid-feedback d-block">
            E-mail inválido!
        </div>
        );
    }
    };

    const vusername = (value) => {
    if (value.length < 3 || value.length > 20) {
        return (
        <div className="invalid-feedback d-block">
            O nome deve ter entre 3 e 20 caracteres!
        </div>
        );
    }
    };

    const vpassword = (value) => {
    if (value.length < 6 || value.length > 40) {
        return (
        <div className="invalid-feedback d-block">
            A password deve ter entre 6 e 40 caracteres!.
        </div>
        );
    }
    };

    const Register = (props) => {
    const form = useRef();
    const checkBtn = useRef();
    const navigate = useNavigate();

    const [name, setName] = useState("");
    const [email, setEmail] = useState("");
    const [password, setPassword] = useState("");
    const [successful, setSuccessful] = useState(false);
    const [message, setMessage] = useState("");

    const handleRegister = (e) => {
        e.preventDefault();

        setMessage("");
        setSuccessful(false);

        form.current.validateAll();

        if (checkBtn.current.context._errors.length === 0) {
        AuthService.register(name, email, password).then(
            (response) => {
            navigate("/dashboard");
            },
            (error) => {
            const resMessage =
                (error.response &&
                error.response.data &&
                error.response.data.message) ||
                error.message ||
                error.toString();

            setMessage(resMessage);
            setSuccessful(false);
            }
        );
        }
    };

    return (
        <main>
        <section>
        <div className="p-5 mb-4 bg-body-tertiary rounded-3">
            <div className="container-fluid py-5">
                <Form onSubmit={handleRegister} ref={form} className="col-4">
                {!successful && (
                    <div>
                    <h1 className="h3 mb-3 fw-normal">Registar</h1>

                    <div className="form-group">
                        <label>Nome</label>
                        <Input
                        type="text"
                        className="form-control"
                        name="name"
                        value={name}
                        onChange={(e) => setName(e.target.value)}
                        validations={[required, vusername]}
                        />
                    </div>

                    <div className="form-group">
                        <label>Email</label>
                        <Input
                        type="text"
                        className="form-control"
                        name="email"
                        value={email}
                        onChange={(e) => setEmail(e.target.value)}
                        validations={[required, validEmail]}
                        />
                    </div>

                    <div className="form-group">
                        <label>Password</label>
                        <Input
                        type="password"
                        className="form-control"
                        name="password"
                        value={password}
                        onChange={(e) => setPassword(e.target.value)}
                        validations={[required, vpassword]}
                        />
                    </div>

                    <div className="form-group">
                        <button className="btn btn-success mt-2">Registar</button>

                        <Link to={"/"} className="btn btn-secondary mt-2 mx-2">
                        Voltar
                        </Link>
                    </div>
                    </div>
                )}

                {message && (
                    <div className="form-group">
                    <div
                        className={
                        successful ? "alert alert-success" : "alert alert-danger"
                        }
                        role="alert"
                    >
                        {message}
                    </div>
                    </div>
                )}
                <CheckButton style={{ display: "none" }} ref={checkBtn} />
                </Form>
            </div>
            </div>
        </section>
        </main>
    );
    };

    export default Register;
    ```

- Criar uma página Dashboard /src/components/secure/Dashboard.jsx

    ### Dashboard.jsx

    ```jsx
    import React from "react";
    import AuthService from "../../services/auth.service";
    import { useNavigate, Link } from "react-router-dom";

    const Dashboard = () => {
        const navigate = useNavigate();
        const currentUser = AuthService.getCurrentUser();

        const logOut = () => {
            AuthService.logout();
            navigate('/');
        };

        return (
            <main>
                <div className="p-1 mb-4 bg-body-tertiary rounded-3">
                    <div className="container-fluid py-5">
                        <h1 className="display-5 fw-bold">Hello {currentUser}</h1>
                        <p className="col-md-8 fs-4">Ready for today?</p>
                        <div className="d-flex justify-content">
                            <button className="btn btn-danger btn-lg px-4" onClick={logOut}>Terminar sessão</button>
                        </div>
                    </div>
                </div>
            </main>
        );
    };

    export default Dashboard;

    ```

- Alterar o App.js para as rotas:

    ```jsx
    import React, {  } from "react";
    import { Route, Routes, Navigate } from "react-router-dom";
    import "bootstrap/dist/css/bootstrap.min.css";
    import "./App.css";

    import PrivateRoutes from "./utils/privateRoute";
    import PublicRoutes from "./utils/publicRoute";

    //PUBLIC ROUTES
    import Home from "./components/public/Home";
    import Login from "./components/public/Login";
    import Register from "./components/public/Register";

    //PRIVATE ROUTES
    import Dashboard from "./components/secure/Dashboard";
    import Footer from "./components/shared/Footer";
    import Header from "./components/shared/Header";

    const App = () => {
    return (
        <div>
        <div className="container mt-3">
        <Header /> 
            <Routes>
            <Route element={<PrivateRoutes />}>
                <Route path="/dashboard" element={<Dashboard />} />
                <Route path='*'element={<Navigate to="/dashboard" />} />
            </Route>

            <Route element={<PublicRoutes />}>
                <Route exact path={"/"} element={<Home />} />
                <Route exact path="/login" element={<Login />} />
                <Route exact path="/register" element={<Register />} />
                <Route path="*" element={<Navigate to="/" />}  />
            </Route>
            </Routes>
            <Footer /> 
        </div>
        </div>
    );
    };

    export default App;
    ```

- Testar:

    ```bash
    npm run dev
    ➜  Local:   http://localhost:5174/
    ```

## Aula 4 - CRUD

- Criar os componentes de 

    ### StudentsList.jsx

    ```jsx
    import React, { useState, useEffect } from 'react';
    import StudentsService from "../../../services/students.service";
    import { Link } from 'react-router-dom';

    const StudentsList = () => {
        const [students, setStudents] = useState([]);

        useEffect(() => {
            async function fetchData() {
                const data = await StudentsService.getAll();
                setStudents(data.data);
            }

            fetchData();
        }, []);

        return (
            <main>
                <section className="py-4">
                    <div className="d-flex justify-content">
                        <Link to={"/"} className="btn btn-secondary px-4 mx-2">
                            Voltar
                        </Link>

                        <Link to={"/student"} className="btn btn-success px-4 mx-2">
                            Registar
                        </Link>
                    </div>
                </section>

                <section>
                    <table className="table table-dark table-hover">
                        <thead>
                            <tr>
                                <th scope="col">#</th>
                                <th scope="col">Nome</th>
                                <th scope="col">Número</th>
                                <th scope="col">Cidade</th>
                                <th scope="col">Aniversário</th>
                                <th scope="col"></th>
                            </tr>
                        </thead>

                        <tbody>
                            {students.map((student, index) => (
                                <tr key={student.id}>
                                    <td >{index + 1}</td>
                                    <td>{student.name}</td>
                                    <td>{student.number}</td>
                                    <td>{student.city}</td>
                                    <td>{student.birthday}</td>
                                    <td>
                                        <div className="d-flex justify-content">
                                            <Link to={`/student/${student.number}`} className='btn btn-primary me-2'>Editar</Link>
                                        </div>
                                    </td>
                                </tr>
                            ))}
                        </tbody>
                    </table>
                </section>
            </main>
        );
    }

    export default StudentsList;
    ```

    ### Student.jsx

    ```jsx
    import React, { useState, useRef, useEffect } from 'react';
    import { Navigate, useParams, useNavigate } from "react-router-dom";
    import Form from "react-validation/build/form";
    import Input from "react-validation/build/input";
    import CheckButton from "react-validation/build/button";
    import { Link } from "react-router-dom";

    import StudentsService from "../../../services/students.service";

    const Student = () => {
        const navigate = useNavigate();


        const params = useParams();
        const [id, setId] = useState(null);
        const [number, setNumber] = useState("");
        const [name, setName] = useState("");
        const [city, setCity] = useState("");
        const [birthday, setBirthday] = useState("");
        const [successful, setSuccessful] = useState(null);
        const [message, setMessage] = useState("");

        useEffect(() => {
            if (!params.number) {
                return;
            }

            async function fetchData() {
                const response = await StudentsService.getById(params.number);

                setId(response.data.id);
                setNumber(response.data.number);
                setName(response.data.name);
                setCity(response.data.city);
                setBirthday(response.data.birthday);
            }

            fetchData();
        }, []);


        const form = useRef();
        const checkBtn = useRef();

        const handleRegister = (e) => {
            e.preventDefault();

            setMessage("");
            setSuccessful(false);

            form.current.validateAll();

            if (checkBtn.current.context._errors.length === 0) {
                StudentsService.createORupdate(id, number, name, city, birthday).then(
                    (response) => {
                        setMessage(response.data.message);
                        setSuccessful(true);

                        setId(response.data.id);
                        setNumber(response.data.number);
                        setName(response.data.name);
                        setCity(response.data.city);
                        setBirthday(response.data.birthday);
                    },
                    (error) => {
                        const resMessage =
                            (error.response &&
                                error.response.data &&
                                error.response.data.message) ||
                            error.message ||
                            error.toString();

                        setMessage(resMessage);
                        setSuccessful(false);
                    }
                );
            }
        };

        const handleDelete = (e) => {
            e.preventDefault();

            StudentsService.deleteUser(number).then(
                (response) => {
                    navigate('/students-list');
                },
                (error) => {
                    const resMessage =
                        (error.response &&
                            error.response.data &&
                            error.response.data.message) ||
                        error.message ||
                        error.toString();

                    setMessage(resMessage);
                    setSuccessful(false);
                }
            );
        }

        const required = (value) => {
            if (!value) {
                return (
                    <div className="invalid-feedback d-block">
                        É obrigatório!
                    </div>
                );
            }
        };

        const validLength = (value) => {
            if (value.length < 3 || value.length > 50) {
                return (
                    <div className="invalid-feedback d-block">
                        O nome deve ter entre 3 e 20 caracteres!
                    </div>
                );
            }
        };

        return (
            <main>
                <section>
                    <div className="p-5 mb-4 bg-body-tertiary rounded-3">
                        <div className="container-fluid py-5">
                            <Form onSubmit={handleRegister} ref={form} className="col-4">
                                <div>
                                    <h1 className="h3 mb-3 fw-normal">Registar</h1>

                                    <div className="form-group">
                                        <label>Número</label>
                                        <Input
                                            type="text"
                                            className="form-control"
                                            name="number"
                                            value={number}
                                            onChange= {(e) => setNumber(e.target.value)}
                                            validations={[required]}
                                        />
                                    </div>

                                    <div className="form-group">
                                        <label>Nome</label>
                                        <Input
                                            type="text"
                                            className="form-control"
                                            name="name"
                                            value={name}
                                            onChange={(e) => setName(e.target.value)}
                                            validations={[required, validLength]}
                                        />
                                    </div>

                                    <div className="form-group">
                                        <label>Cidade</label>
                                        <Input
                                            type="text"
                                            className="form-control"
                                            name="city"
                                            value={city}
                                            onChange={(e) => setCity(e.target.value)}
                                            validations={[required, validLength]}
                                        />
                                    </div>

                                    <div className="form-group">
                                        <label>Aniversário</label>
                                        <Input
                                            type="text"
                                            className="form-control"
                                            name="birthday"
                                            value={birthday}
                                            onChange={(e) => setBirthday(e.target.value)}
                                            validations={[required]}
                                        />
                                    </div>

                                    <div className="form-group">
                                        <button className="btn btn-success mt-2">Registar</button>

                                        {id && (<button onClick={handleDelete} className="btn btn-danger mt-2 mx-2">
                                            Eliminar
                                        </button>)}

                                        <Link to={"/students-list"} className="btn btn-secondary mt-2 mx-2">
                                            Voltar
                                        </Link>
                                    </div>
                                </div>

                                {successful && (
                                    <div className="alert alert-success mt-2" role="alert">
                                        Gravado com sucesso!
                                    </div>
                                )}


                                {message && successful !== null && (
                                    <div className="form-group">
                                        <div
                                            className={
                                                successful ? "alert alert-success" : "alert alert-danger"
                                            }
                                            role="alert"
                                        >
                                            {message}
                                        </div>
                                    </div>
                                )}
                                <CheckButton style={{ display: "none" }} ref={checkBtn} />
                            </Form>
                        </div>
                    </div>
                </section>
            </main>
        );
    }

    export default Student;
    ```

- Criar o serviço de students (src/services/students.service.js)

    ### auth.service.js

    ```jsx
    import axios from "axios";

    const API_URL = "https://aw-p-exemplo-1778.vercel.app/api/v2/students/";

    axios.interceptors.request.use(
    config => {
        config.headers['Authorization'] = `Bearer ${localStorage.getItem('token')}`;
            return config;
        },
        error => {
            return Promise.reject(error);
        }
    );

    const getAll = () => {
    return axios.get(API_URL);
    };

    const getById = (number) => {
    return axios.get(API_URL + number);
    };

    const createORupdate = (id, number, name, city, birthday) => {
    if(id == null){
        return create(number, name, city, birthday);
    }
    else {
        return update(id, number, name, city, birthday);
    }
    };

    const create = (number, name, city, birthday) => {
    return axios.post(API_URL + "create", { number, name, city, birthday });
    };

    const update = (id, number, name, city, birthday) => {
    return axios.put(API_URL + "update", { id, number, name, city, birthday });
    };

    const deleteUser = (number) => {
    return axios.delete(API_URL + "delete/" + number);
    };

    const StudentsService = {
    getAll,
    getById,
    createORupdate,
    create,
    update,
    deleteUser
    }

    export default StudentsService;
    ```

- Alterar o App.jsx com as novas rotas

    ```jsx
    import React, {  } from "react";
    import { Route, Routes, Navigate } from "react-router-dom";
    import "bootstrap/dist/css/bootstrap.min.css";
    import "./App.css";

    import PrivateRoutes from "./utils/privateRoute";
    import PublicRoutes from "./utils/publicRoute";

    //PUBLIC ROUTES
    import Home from "./components/public/Home";
    import Login from "./components/public/Login";
    import Register from "./components/public/Register";

    //PRIVATE ROUTES
    import Dashboard from "./components/secure/Dashboard";
    import StudentsList from "./components/secure/students/StudentsList";
    import Student from "./components/secure/students/Student";

    import Footer from "./components/shared/Footer";
    import Header from "./components/shared/Header";

    const App = () => {
    return (
        <div>
        <div className="container mt-3">
        <Header /> 
            <Routes>
            <Route element={<PrivateRoutes />}>
                <Route path="/dashboard" element={<Dashboard />} />
                <Route path="/students-list" element={<StudentsList />} />
                <Route path="/student" element={<Student />} />
                <Route path="/student/:number" element={<Student />} />
                <Route path='*'element={<Navigate to="/dashboard" />} />
            </Route>

            <Route element={<PublicRoutes />}>
                <Route exact path={"/"} element={<Home />} />
                <Route exact path="/login" element={<Login />} />
                <Route exact path="/register" element={<Register />} />
                <Route path="*" element={<Navigate to="/" />}  />
            </Route>
            </Routes>
            <Footer /> 
        </div>
        </div>
    );
    };

    export default App;
    ```

- A alterar o Dashboard

    ```jsx 
    import React from "react";
    import AuthService from "../../services/auth.service";
    import { useNavigate, Link } from "react-router-dom";

    const Dashboard = () => {
        const navigate = useNavigate();
        const currentUser = AuthService.getCurrentUser();

        const logOut = () => {
            AuthService.logout();
            navigate('/');
        };

        return (
            <main>
                <div className="p-1 mb-4 bg-body-tertiary rounded-3">
                    <div className="container-fluid py-5">
                        <h1 className="display-5 fw-bold">Hello {currentUser}</h1>
                        <p className="col-md-8 fs-4">Ready for today?</p>
                        <div className="d-flex justify-content">
                            <button className="btn btn-danger btn-lg px-4" onClick={logOut}>Terminar sessão</button>

                            <Link to={'/students-list'} className="btn btn-info btn-lg px-4 mx-2">
                                Alunos
                            </Link>
                        </div>
                    </div>
                </div>
            </main>
        );
    };

    export default Dashboard;
    ```

- Testar:

    ```bash
    npm run dev
    ➜  Local:   http://localhost:5174/
    ```