<template>
    <div> 
        这是每个复用该组件都显示的
        <slot></slot>
        <slot name="slot1"></slot>
        <slot name="slot2"></slot>
        <slot name="slot3"></slot>
    </div>
</template>