FROM hugomods/hugo:latest


# Install common packages
RUN apk add curl git make wget vim bat zoxide eza zsh openssh

# Install ZSH, Oh My Zsh, p10k and ZSH-Autosuggestions
RUN git clone -b v5 https://github.com/romkatv/zsh4humans.git /zsh4humans \
    && cp /zsh4humans/.zshenv ~/.zshenv \
    && rm -rf /zsh4humans

# Add customization settings to ZSH
RUN wget https://gist.githubusercontent.com/OliRafa/f39d29a34f38edf4a9c9a2f6dd092260/raw/.p10k.zsh -O ~/.p10k.zsh \
    && wget https://gist.githubusercontent.com/OliRafa/f39d29a34f38edf4a9c9a2f6dd092260/raw/.zshrc -O ~/.zshrc

# Make ZSH the default shell
RUN apk add --update libuser \
    # create necessary files to change the default shell
    && touch /etc/login.defs \
    && mkdir /etc/default \
    && touch /etc/default/useradd \
    # change the password of teh current user to ''
    && passwd `whoami` -d \
    # change the default shell to zsh for the current user
    && echo '/bin/zsh' | lchsh `whoami`

# Installing Commitizen for standardizing commit messages
RUN apk add py3-pip \
    && pip install --no-cache-dir --break-system-packages commitizen ipython
