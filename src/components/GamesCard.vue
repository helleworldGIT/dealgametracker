<template>
    <div v-show="showData">
        <!-- GAMECARD CON LA INFO DE LOS/EL JUEGO RESULTADO DE LA BÚSQUEDA -->
        <h2>
            The games you were looking for: 👇
        </h2>
        <div class="gameCard" v-for="game in games" :key="game.id">
            <router-link :to="{ name:'Game', params: {id: game.gameID}}">
                <div class="onsale">
                    <p :class="{hide: game.isOnSale === 0 
                    || game.isOnSale === '0' 
                    ||  game.isOnSale === false 
                    ||  game.isOnSale === 'false', 
                    show: game.isOnSale === 1 
                    || game.isOnSale === '1' 
                    ||  game.isOnSale === true 
                    ||  game.isOnSale === 'true', }">
                        ON SALE! 💡
                    </p>
                </div>
                <p class="game_title_appear">
                    📍 {{game.title.toUpperCase()}}
                </p>
                <div class="gameContainer">
                    <div class="gameInfo">
                        <p>
                            <span>
                                Deal:
                            </span>
                            💰{{game.salePrice}} €
                        </p>
                        <p :class="{hide: game.steamRatingText === null}">
                            <span>
                                Steam rating⭐:
                            </span>
                            {{game.steamRatingText}}
                        </p>
                    </div>
                    <img alt="Game cover image" title="Game cover image" :src="game.thumb">
                </div>
                <router-link :to="{ name:'Game', params: {id: game.gameID}}">
                    <button>
                            CHECK DEALS
                    </button>
                </router-link>
            </router-link>      
        </div>
        <!-- /GAMECARD CON LA INFO DE LOS/EL JUEGO RESULTADO DE LA BÚSQUEDA -->
    </div>
</template>

<script>
    export default {
        name: 'GameCard',
        props: {
            games: Array,
            showData: Boolean
        }
    }
</script>

<style lang="scss" scoped>
@import "../css/responsive";

    .game_title_appear {
        color: #f7f7f7;
        padding: 0.8rem;
    }

    .onsale {
        width: auto;
        border: none;
        background: #221f3b;
        color: #eebb4d;
        font-size: 0.9rem;
        border-radius: 10px 10px 0 0;
    }

    .hide {
        display: none;
    }

    .show {
        display: inline-block;
    }

    h2 {
        color: #fdcb9e;
        padding: 1rem;
    }

    .gameCard {
        display: inline-block;
        margin-top: 1rem;
        margin-bottom: 1rem;
        margin-right: 1rem;
        margin-left: 1rem;
        width: 320px;
        animation-name: gamesAppear;
        animation-duration: 1s;
        background: #3b2e5a;
        border-radius: 10px;
        transition: all .2s;
        @include xs-screen {
            width: 270px;
        }
        &:hover {
            transform: translateY(-5px);
            background: #00005c;
        }
        button {
            width: 100%;
            padding: 0.667rem;
            border: none;
            background: #6a097d;
            color: #ffdcb4;
            &:hover {
                background: #00005c;
                cursor: pointer;
                font-weight: bold;
            }
        }
        a {
            text-decoration: none;
            font-size: 1rem;
        }
    }

    .gameContainer {
        padding: 0.167rem;
        display: flex;
        justify-content: center;
        img {
            display: block;
            width: 120px;
            height: 100%;
            padding: 1rem;
        }
        .gameInfo {
            text-align: center;
            padding: 0.667rem;
            .title{
                font-size: 1.2rem;
            }
        }
        span {
            font-weight: bold;
            color: #e7dfd5;
            display: block;
            margin-left: 10px;
            @include xs-screen {
                font-size: 0.8rem;
            }
        }
        p {
            color: #bbe1fa;
            margin-left: 10px;
            @include xs-screen {
                font-size: 0.8rem;
            }
        }
    }

    @keyframes gamesAppear {
        from {opacity: 0; margin-top: 2rem;};
        to {opacity: 1; margin-top: 1rem;};
    }

</style>