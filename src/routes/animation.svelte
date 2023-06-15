    <script>
    export let name;
    </script>

    <main>
    <h1>Welcome to my chat app! Im {name} nice to meet u</h1>
    <span>👋</span>
    </main>
    <style>
    main {
        position: absolute;
        top: 0;
        right: 0;
        height: 100vh;
        width: calc(100vw - 300px);
        user-select: none;
        pointer-events: none;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: #333;
    }
    span {
        animation-name: wave-animation;
        animation-duration: 1s;
        animation-iteration-count: infinite;
        transform-origin: 70% 70%;
        display: inline-block;
        font-size: 50px;
    }
    h1 {
        color: white;
        font-size: 25px;
    }

    @keyframes wave-animation {
        0% {
        transform: rotate(0deg);
        }
        25% {
        transform: rotate(10deg);
        }
        50% {
        transform: rotate(0deg);
        }
        75% {
        transform: rotate(70deg);
        }
        1000% {
        transform: rotate(-50deg);
        }
    }
    </style>
