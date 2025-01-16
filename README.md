## Tailwind CLI STDOUT bug

Running the CLI with an empty `-o` option creates a file called 
[`./true`](https://github.com/vormwald/tailwind-stdout-bug/blob/714c8a50dbd4aad779c7241c23607b7367a939a9/v4/true) which contains the generated CSS content.

### [Version 3](https://github.com/vormwald/tailwind-stdout-bug/tree/714c8a50dbd4aad779c7241c23607b7367a939a9/v3)

```shell
cd v3/
npx tailwindcss -h
#=> tailwindcss v3.4.17

npx tailwindcss -i ./input.css
#=> see generated tailwind output
```

### [Version 4](https://github.com/vormwald/tailwind-stdout-bug/tree/714c8a50dbd4aad779c7241c23607b7367a939a9/v4)

```shell
cd v4 
# install latest betas
npm install tailwindcss@next @tailwindcss/cli@next

npx tailwindcss -h
#=> ≈ tailwindcss v4.0.0-beta.9

# try the same 
npx @tailwindcss/cli@next --i ./input.css
# =>displays the usage output

# add a `-o` 
npx @tailwindcss/cli@next --input ./input.css -o
# => creates a new file named ./true with all the tailwind data

head true
# => /*! tailwindcss v4.0.0-beta.9 | MIT License | https://tailwindcss.com */
    @layer theme, base, components, utilities;
    @layer theme {
      :root {
        --font-sans: ui-sans-serif, system-ui, sans-serif, "Apple Color Emoji",
          "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";

# remove that file
rm -f ./true 

# specify an output file
npx @tailwindcss/cli -i input.css -o output.css
# => works as expected
```

