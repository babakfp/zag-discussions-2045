<script lang="ts">
    import * as radio from "@zag-js/radio-group"
    import { mergeProps, normalizeProps, useMachine } from "@zag-js/svelte"

    const items = ["Apples", "Oranges", "Mangoes", "Grapes"]

    const [snapshot, send] = useMachine(
        radio.machine({ id: "1", name: "fruit" }),
    )

    const api = $derived(radio.connect(snapshot, send, normalizeProps))
</script>

<div {...api.getRootProps()}>
    <h3 {...api.getLabelProps()}>Fruits</h3>
    {#each items as value}
        <label {...api.getItemProps({ value })}>
            <span {...api.getItemTextProps({ value })}>{value}</span>

            {console.log("1", api.getItemHiddenInputProps({ value }).style)}
            {console.log(
                "2",
                mergeProps(api.getItemHiddenInputProps({ value }), {}).style,
                // NOTE: If you remove `{}` it doesn't happen
            )}
            <input {...api.getItemHiddenInputProps({ value })} />

            <div {...api.getItemControlProps({ value })}></div>
        </label>
    {/each}
</div>
